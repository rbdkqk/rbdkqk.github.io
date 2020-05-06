---
title:  "\"코드 테스트하기\"와 \"문법 교정하기\""
excerpt: "Jest & ESLint"

categories:
  - studynote
tags:
  - Javascript
  - linter & test
last_modified_at: 2020-05-06
---


<br>


# Jest - "코드의 기능 테스트"

## 1. 테스트 도구의 필요성  

&nbsp;Javascript를 공부하면서, 어떤 문제를 만나면 나름의 방법으로 코드를 작성하고 이 코드가 원하는 방향대로 잘 실행되는지 아닌지를 테스트할 일이 많이 있었습니다.  

&nbsp;이럴 때, 제가 주로 선택한 방법은 다음과 같습니다.  
    
- 크롬 개발자 도구를 열고, 빈 콘솔 창에 작성한 코드를 붙여넣기  
    
- 테스트하고 싶은 예시 역시 그 밑에 함께 붙여넣기  
    
- 테스트에 사용할 위 예시를 반영해서 해당 코드를 실행시켜 보고, 원하는 결과가 나오지 않으면 코드를 수정하여 다시 처음부터 반복  
    
&nbsp;이렇게 하여 오류를 교정해 나가는 방식을 취했습니다. 굉장히 비효율적이라고 생각했습니다만, 코드가 잘 작동하는지를 보다 효율적으로 체크할 방법은 찾아볼 생각도 하지 못하고 있었습니다.  
    
&nbsp;그러나, 이번 공부를 통해 터미널에서 명령어 하나로 이런 테스트를 해낼 수 있다는 것을 알게 되었습니다.  
    
&nbsp;이하에서는 이런 기능을 수행할 수 있는 Jest에 관하여 기록해 두려고 합니다.

## 2. "Jest" 설치 및 적용  

(1) 테스트의 대상이 될 코드를 작성합니다.  
&nbsp;해결해야 하는 또는 작성해야 하는 코드를 작성합니다. 이는 어떠한 기능을 해낼 수 있는 함수를 작성한다던가 하는 것입니다.  
&nbsp;(예를 들면 다음과 같습니다.)
```js
function sum(a, b) {
  return a + b;
}
module.exports = sum;
```  

<!--
`module.exports`는 다음과 같은 기능을 수행합니다.  
- 

-->


(2) 위 코드를 테스트하기 위한 테스트케이스를 작성합니다.  
&nbsp;(예를 들면 다음과 같습니다.)
```js
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

<!--
`const sum = require('./sum')` 부분은 다음과 같은 기능을 수행합니다.
 - 

-->

&nbsp;test 이하 부분의 내용은 다음과 같습니다.
- test : 이하의 내용을 테스트하는 기능을 제공합니다.
- expect : 안의 내용을 실행한 결과입니다. 주어진 코드를 실행한 결과이며, toBe 부분의 값과 비교하게 됩니다.
- toBe : 실행결과로 기대되는, 즉 개발자가 의도한 값을 입력합니다. 




(3) 위 두 사항이 포함된 프로젝트 디렉토리에, Jest를 설치합니다.  
&nbsp;(Jest 설치를 위해, [공식 문서](https://jestjs.io/)를 참고했습니다.)  
- 'npm'을 활용하여, `npm install --save-dev jest` 명령어를 입력합니다.  
- 테스트 대상인 코드와 테스트케이스를 위와 같이 작성합니다.  
- `package.json` 파일을 열고, Jest 적용을 위해 다음과 같은 내용을 추가합니다. 이것은 `"test"라는 명령어로 "jest"를 실행하라`는 기능을 추가해 주는 것입니다.  

```js
{
    "scripts": {
    "test": "jest"
    }
}
```

- 이후, 터미널에 `npm run test` 라는 명령어를 입력하면, Jest를 활용하여 위 코드를 테스트한 결과를 출력해 줍니다.  

```js
function countWords(input) {
  return (input === null)
    ? {}
    : input.split(" ").reduce((resultObj, key) => {
      resultObj[key] ? resultObj[key]++ : resultObj[key] = 1;
      return resultObj;
    }, {});   
}
```  
&nbsp;예를 들어 위와 같은 코드를 작성한 뒤, (두번째 줄을 `return (input === "")` 으로 작성해야 동작하지만, 테스트에 실패하도록 하기 위해 `return (input === null)`로 변경했습니다.)  

&nbsp;그 뒤 `npm run test` 명령어를 입력하면,

```js
 FAIL  pass-me/__test__/countWords.test.js
  ● countWords › 빈 문자열을 넘겼을 때는 빈 객체를 리턴해야 합니다

    expect(received).toEqual(expected) // deep equality

    - Expected  - 1
    + Received  + 3

    - Object {}
    + Object {
    +   "": 1,
    + }
```  

&nbsp;이런 식으로 에러메세지가 출력됩니다.  

&nbsp;이는 `countWords.test.js 파일에서 expected 값과 received 값이 이와 같이 다르다`는 메세지이므로, 코드를 적절하게 수정하면,  

```js
 PASS  pass-me/__test__/countWords.test.js
```  

&nbsp;이런 통과 메세지를 볼 수 있습니다.  

- 이렇게 하여, 기본적인 Jest 사용이 가능해졌습니다.  [공식 문서](https://jestjs.io/)를 참고하면 더 많은 기능을 확인할 수 있으니, 이에 관하여도 더 공부하여 이 아래에 추가하려고 합니다.  


## 3. 참고자료  
&nbsp;Jest의 사용 등에 관하여 다음과 같은 문서들을 참고하여 추가 공부하려고 합니다. (다른 분께서 작성하신 글을 몇 가지 링크하였습니다. 이 부분의 삭제요청이 들어온다면 즉시 반영하도록 하겠습니다.)  
 - [Jest 공식 문서](https://jestjs.io/)  
 - [Jest - API Reference(공식 문서)](https://jestjs.io/docs/en/api)  
 - [facebook/jest](https://github.com/facebook/jest) 
 - [Jest로 기본적인 테스트 작성하기](https://www.daleseo.com/jest-basic/)  
 - [Jest Tutorial for Beginners: Getting Started With JavaScript Testing](https://www.valentinog.com/blog/jest/)  
 - [[Jest] Javascript Test 코드 작성하기](https://hees-dev.tistory.com/57)  
 - [Jest로 테스트 전/후 처리하기](https://www.daleseo.com/jest-before-after/)  

 

<!--
## 3. Jest 공식문서 살펴보기


-->

<br>  

# ESLint - "코드의 문법 테스트"

## 1. linter의 필요성

&nbsp;프로그래밍을 위한 코딩 작업은 혼자 할 수도 있고, 여러 사람이 협업하여 결과를 만들 수도 있습니다.  

&nbsp;보통은 협업을 하게 될 텐데, 똑같은 코드를 작성하더라도 참여하는 사람마다 각자 다른 방식으로 표시하기 마련입니다.  
 - 가령 저는 변수의 이름으로 주로 '카멜케이스(formValue)' 방식을 취하지만, 어떤 사람은 '언더바(form_value)' 형식을 선호할 수도 있고, 어떤 사람은 이런 것을 신경쓰지 않고 그냥 길게 늘여 쓸 수도 있습니다.  
 - 함수 안의 내용이 간단한 경우, 어떤 사람은 한 줄에 모두를 표기하기를 원할 수도 있지만, 저는 가급적 `{` 기호와 `}` 기호를 각각 별도의 줄에 표기하고 있습니다.  

&nbsp;이렇게 모두가 각자의 다른 방식으로 코드를 작성한다면, 협업 과정에서 서로의 코드를 알아보지 못하여 어려움을 겪을 수 있을 것입니다.  

&nbsp;또한, 협업이 아니라 혼자 코드를 작성하는 경우라도, 시간이 지나 자신의 코드를 돌아보아야 할 때가 오면, 본인이 작성한 코드인데도 스스로조차 알아보기 어려운 경우가 생길 수 있습니다.  

&nbsp;이런 문제를 해결하기 위해, 즉 원활한 협업 환경을 구성하고 유지보수를 보다 편리하게 하기 위해, 코드를 '작성하는 규칙'을 사전에 정해두고 이렇게 통일된 형태를 취할 필요가 있습니다.  

&nbsp;이런 목적을 위해서 만들어진 여러 툴이 있습니다. 그 중 아래에서는 'ESLint'에 관하여 알아보고자 합니다.  

## 2. ESLint 설치 및 적용

&nbsp;설치와 설정을 위해, [ESLint](https://eslint.org/docs/user-guide/getting-started)의 공식문서를 참고하였습니다.

&nbsp;`eslint --init` 명령어를 실행하여 `.eslintrc` 라는 설정 파일을 만든 뒤, `"rules":` 부분 안에 일정한 규칙을 정해줄 수 있습니다.  

```js
{
    "rules": {
        "semi": ["error", "always"],
        "quotes": ["error", "double"]
    }
}
```  

&nbsp;이와 같이 작성하면, "semi" , "quotes" 등의 규칙에 관한 처리를 지정해 줄 수 있습니다.  

&nbsp;첫번째 자리의 `"error"` 는 에러의 레벨을 지정해 주는 곳입니다. `"off" / "warn" / "error"`의 3가지 경우 중 하나로 설정해 줄 수 있습니다.  


```js
{
    "extends": "eslint:recommended"
}
```  

&nbsp;이와 같이 작성하면, [rules page](https://eslint.org/docs/rules/)에 정리되어 있는 ESLint의 기본적인 규칙들을 자동으로 모두 적용해 줍니다. 이외에도 다양한 규칙이 있으므로 이를 적용할 수 있습니다.  


&nbsp;이렇게 설정한 뒤, `package.json` 파일의 `"scripts"` 부분에 `"lint"` 명령어에 대한 실행내용을 설정해 줘야 합니다.

```js
"scripts": {
    "lint": "eslint",
  },
```

&nbsp;이렇게 설정하면 프로젝트의 모든 파일에 대하여 ESlint를 실행합니다.


&nbsp;이제, 아래와 같이 작성한 코드를 ESLint를 활용하여 테스트해 볼 수 있습니다.  

```js
function countWords(input) {
  return (input === "")
    ? {}
    : input.split(" ").reduce((resultObj, key) => {
      resultObj[key] ? resultObj[key]++ : resultObj[key] = 1;
      return resultObj
    }, {});   
}
```

&nbsp;`return resultObj` 부분의 가장 끝 자리에 들어갈 `;` 기호를 일부러 지우고, `npm run lint` 명령어를 입력하여 ESLint를 실행하면,  

```js
/home/rbdkqk/Desktop/rbdkqk/im-sprints-immersive-prep/pass-me/countWords.js
  22:23  error  Missing semicolon  semi
```  

&nbsp;이런 에러메세지가 출력됩니다.  

&nbsp;`countWords.js 코드의 22번째 줄 23번째 칸에, semicolon이 없는 문제가 있어 에러가 발생했다`  는 에러메세지가 출력되었습니다.  

&nbsp;이런 에러메세지를 확인하여 해당 코드를 찾아가서 지적된 오류를 수정할 수 있게 됩니다.  

## 3. 참고자료 

&nbsp;ESlint의 사용 등에 관하여 다음과 같은 문서들을 참고하여 추가 공부하려고 합니다. (다른 분께서 작성하신 글을 몇 가지 링크하였습니다. 이 부분의 삭제요청이 들어온다면 즉시 반영하도록 하겠습니다.)  
 - [ESLint 공식문서](https://eslint.org/docs/user-guide/getting-started)  
 - [ESLint 공식문서 - Specifying Globals](https://eslint.org/docs/user-guide/configuring#specifying-globals)  
 <!--   /* global var1, var2 */ 부분 공부해야 함    -->
 - [Configuring ESLint - Specifying Environments](https://eslint.org/docs/user-guide/configuring#specifying-environments)  
 - [[자바스크립트] ESLint로 소스 코드의 문제 찾기](https://www.daleseo.com/js-eslint/)  
 - [linter를 이용한 코딩스타일과 에러 체크하기](https://subicura.com/2016/07/11/coding-convention.html)  
 - [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)  
 - [Airbnb JavaScript 스타일 가이드(번역)](https://github.com/ParkSB/javascript-style-guide)  
 - [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)  
 - [ESLint(TSLint)와 Prettier 함께 사용하기](https://pravusid.kr/javascript/2019/03/10/eslint-prettier.html)  
 - [VS Code에서 ESLint 사용하기 - 1. 기본 설정](https://noooop.tistory.com/entry/VS-Code%EC%97%90%EC%84%9C-ESLint-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-1-%EA%B8%B0%EB%B3%B8-%EC%84%A4%EC%A0%95)  


<!--
## 3. ESLint 공식문서 살펴보기


-->