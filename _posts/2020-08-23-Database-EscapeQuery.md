---
title:  "Database - MySQL"
excerpt: "query() 메소드의 문법"

categories:
  - studynote
tags:
  - Javascript
  - Database
  - MySQL
last_modified_at: 2020-08-23
---

# &nbsp;&nbsp; MySQL - `query()` 메소드 

MySQL을 활용한 Database 공부 중, MySQL 모듈을 활용하는 방법과 `query()` 메소드를 작성하는 방법에 관하여 공부하였습니다.   

<br>
---
<br>
<br>


# 1. MySQL 모듈의 기본 사용법

MySQL 모듈을 `const mysql = require('mysql');` 이렇게 설치한 뒤,  

```js
const connection = mysql.createConnection({
  host     : 'localhost',  // 호스트 주소입니다.
  user     : 'me',         // mysql 사용자의 명칭입니다.
  password : 'secret',     // 환경변수로 작성해 준 뒤, 변수로 받아 넣어줄 수 있습니다.
  database : 'my_db'       // mysql 데이터베이스의 이름을 동일하게 넣어줍니다.
});
```  

위와 같이 작성하여 연결시에 사용될 정보를 지정해 주고,  

`connection.connect();` 메소드를 통해서, MySQL 데이터베이스에 연결된 뒤,   

이후, `connection.query()` 메소드를 활용하여 실제로 데이터베이스를 조작하게 됩니다.  

<br>
---
<br>
<br>


# 2. `query()` 메소드 

이 과정 중, 마지막의 `.query()` 메소드는, 
 - 첫번째 매개변수로 `데이터베이스를 조작하는 query`를, 
 - 두번째 매개변수로 `query의 처리 결과를 어떻게 다룰 것인지를 정하는 callback 함수`를 받습니다.  

가령, 서버의 GET 요청에 대응하기 위해서는, 

```js
`messages 라는 table에 GET 요청을 보낼 때,`

get: function () {
      return new Promise((resolve,reject) =>{
        connection.query(`SELECT * FROM messages`, function(err, result){
          if(err) throw err; 
          resolve(result);
        })
      })
    }
```  

이와 같이 `query()` 메소드를 활용할 수 있습니다.  


그런데, 실제로는 매번의 요청마다 각각 다른 query를 작성해 주어야 할 경우를 고려해야 합니다.

가령, 서버의 POST 요청에 대응하려면,  

```js
`POST 요청에서 username, text, roomname 3가지 정보를 포함하는 객체를 보내온다면,`

post: function ( { username, text, roomname } ) {
      return new Promise((resolve,reject) =>{
        let sql = `INSERT INTO 
                    messages (username, text, roomname) 
                    VALUES ( ${username}, ${text}, ${roomname} )` 
        connection.query(sql, function(err, result){
          if(err) throw err; 
          resolve(result);
        })
      })      
    }
```  

이와 같이, POST 요청에서 주어지는 객체(username, text, roomname 3가지 정보를 포함하고 있습니다.)를,  
query 안의 VALUES 위치에 넣어줘야 합니다.  

이렇게 하여, 매번 달라지는 POST 요청에 대응할 수 있습니다.  

<br>
---
<br>
<br>


# 3. `Escape Query`(?)

위 POST 요청에서 주어지는 값을, `query()` 메소드 안에서 처리하는 방법에 관하여, 새로운 방식을 발견하였기에 이를 기록해 둡니다.  

위와 같은 예시에서,  

```js
`POST 요청에서 username, text, roomname 3가지 정보를 포함하는 객체를 보내온다면,`

post: function ( { username, text, roomname } ) {
      return new Promise((resolve,reject) =>{
        let sql = `INSERT INTO 
                    messages (username, text, roomname) 
                    VALUES ( ?, ?, ? )`
        var queryArgs = [ username, text, roomname ];
        connection.query(sql, queryArgs, function(err, result){
          if(err) throw err; 
          resolve(result);
        })
      })      
    }
```  

위와 같이, 
 - query 안에서 다르게 주어야 할 변수 자리에 `?` 라는 물음표를 넣어주고,  
 - 새로운 배열을 선언하여, POST 요청에서 주어진 세부 값들을 순서대로 나열해 주고,  
 - `query()` 메소드의 두번째 매개변수에서 위 배열을 넣어줘서, `?` 자리에 이 배열의 값들을 순차로 대입해 줍니다.  

주어지는 변수를 query 안에 넣어줄 때, `${}`를 활용하지 않고도 보다 간편하게 작성할 수 있었습니다.

`query()` 메소드 외에도, `format()` 이라는 메소드에서도 활용할 수 있는 점을 확인하였습니다.  


이러한 작성방식? 구문? 을 `Escape Query` 라고 하는 것 같은데(정확한 명칭을 잘 모르겠습니다.), 이에 관하여 공부할 수 있는 기회가 되었습니다.  

매개변수를 대입해 주는 기능 외에도, 보안을 강화하는 방법으로도 활용될 수 있는 것 같습니다.  
(아래 참고자료 중 마지막 링크의 내용 역시 공부하겠습니다.)

<br>
---
<br>
<br>


# 4. 참고자료 
 - [[Node.js 8-2강] 다중쿼리 처리 방법, sql에 파라미터 매핑하는 다양한 방법](https://junspapa-itdev.tistory.com/10)  
 - [MySQL Reference - Performing queries](https://github.com/mysqljs/mysql#performing-queries)  
 - [MySQL Reference - Escaping query values](https://github.com/mysqljs/mysql#escaping-query-values)  
 - [MySQL Reference - Escaping query identifiers](https://github.com/mysqljs/mysql#escaping-query-identifiers)  
 - [코드이그나이터 - 데이터베이스 쿼리의 값을 이스케이프 시키기](http://b.redinfo.co.kr/96)  