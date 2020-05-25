---
title:  "OOP(Object Oriented Programming)"
excerpt: "객체 지향 프로그래밍"

categories:
  - studynote
tags:
  - Javascript
  - Inheritance Patterns
  - Object Oriented Programming
last_modified_at: 2020-05-24
---

&nbsp;이 포스팅에서는 "OOP(Object Oriented Programming, 객체 지향 프로그래밍)"에 관하여 다루고자 합니다.  

&nbsp;프로그래머는 프로그래밍을 진행할 때, 일정한 관점을 갖고 문제해결에 접근하게 됩니다. 

&nbsp;'객체 지향 프로그래밍', '함수 지향 프로그래밍', '절차 지향 프로그래밍' 등의, 다양한 프로그래밍 패러다임이 존재합니다.  

&nbsp;아래에서는 '객체 지향 프로그래밍'에 관하여 공부한 내용을 기록해 두겠습니다.  

<br>
---
<br>

# 1. Object (객체)

&nbsp;'객체'란, key와 그에 대응하는 value의 쌍으로 이루어진 데이터 묶음의 형태를 말합니다.  
&nbsp;쌍으로 이루어져 있다는 점에서, 데이터의 나열인 '배열'과 다르고, 데이터의 묶음이라는 점에서, 일반적인 원시 타입 데이터인 '숫자/문자열/boolean' 등과 다르다고 할 수 있습니다.  

&nbsp;기초적인 객체를 작성한다면 다음과 같을 것입니다.  
```js
let obj = {
  "a" : 1 , 
  "b" : true , 
  "c" : "john", 
  5 : function () {
    return this;  },
  6 : function () {
    this["a"] ++;
    this["b"] --;  }
}
```  

&nbsp;위와 같이 작성한다면, `obj`라는 변수에, `{    }` 안의 내용들을, 각각 짝지은 형태로 담은 형태라고 할 수 있습니다.  
&nbsp;위 객체는, 콜론(`:`)을 기준으로 좌측에 정렬된 값이 key이고, 우측에 정렬된 값이 각각의 key에 대응하는 value입니다.  
&nbsp;obj["a"] 등의 형태로 객체 안의 각 값에 접근할 수 있으며, 객체 안에 함수나 다른 객체를 넣는 것 역시 가능합니다.  

&nbsp;객체 안에는 일정한 값(데이터)가 저장될 수도 있고, 어떠한 동작을 하도록 하는 함수가 저장될 수도 있습니다. 전자를 'property', 후자를 'methods' 라고 합니다.  

&nbsp;가령, 위 `obj` 객체 안에서, `"a" : 1 , "b" : true , "c" : "john"` 부분은 일정한 데이터를 담고 있는 property 입니다. 그리고, `5`와 `6`으로 지정된 함수들은 일정한 동작을 하게 하는 methods에 해당합니다.  

<br>
---
<br>

# 2. OOP(Object Oriented Programming)

&nbsp;이는 프로그래밍을 진행하는 여러가지 관점, 철학 등 중 하나입니다.  

&nbsp;프로그래밍 중에 다루거나 처리해야 하는 모든 대상을 Object(객체)로 보고/인식하고, 프로그래밍에 접근하는 방식을 말합니다.  

&nbsp;객체 지향 프로그래밍은 프로그램을 '상호작용하는 집합'으로 보고 접근하는 방법입니다.  

&nbsp;다시 말하여, "모든 것은 객체이다"라는 관점으로 프로그래밍하는 방법입니다. 우리 주변의 실생활에 존재하는 것들을, 그 속성과 기능 등을 반영한 객체로 표현하고, 프로그래밍 안에서 원활하게 사용할 수 있게 됩니다.  

&nbsp;한 부분 안에서 여러가지 기능을 구현하고 여러가지 상황을 해결하려 하지 않고, 작게 나누어 구현한 뒤 이를 모아 큰 기능을 구현하는 방식입니다.  

&nbsp;아래에서는 이러한 객체지향 프로그래밍의 특징에 관하여 알아보겠습니다.  

<br>
---
<br>

# 3. 객체 지향 프로그래밍의 특징

### &nbsp;(1) Encapsulation (캡슐화)

&nbsp;'Encapsulation(캡슐화)'은 어떤 property와 methods를 하나의 객체로 묶어서 표현하는 방식을 말합니다.  

&nbsp;어떠한 사물의 기능을 코드로 표현할 때, 하나하나의 특징을 매번 모두 나열해 주기는 어려우며 이러헤 나열된 특징들이 모두 이 사물(대상)의 속성인지를 알아보기가 굉장하 어려울 수 있습니다.  

```js
let age = 34;
let firstName = "Gyu Hwa";
let lastName = "Kim";
let sayIntroduceHimself = function (age, firstName, lastName) {
  return "Hello! I\'m "+ firstName + " " + lastName +", " + age + "  years old.";
}

let newGH = sayIntroduceHimself(age, firstName, lastName);
```  

&nbsp;명령형 코드를 사용해서 위와 같이 작성하면, 사람이 달라질때마다 모든 코드를 전부 새로 작성해야 합니다.  

&nbsp;하지만, 위 코드를 아래와 같이 작성하면,   

```js
const people = function {
  age : 34,
  firstName = "Gyu Hwa",
  speak : "woof woof!",
  getAnimal: function() {
    return "Hello! I\'m "+ this.firstName + " " + this.lastName +", " + this.age + "  years old.";
  }
}

people.people(); 

```  

&nbsp;위와 같이 작성할 수 있습니다. 이는 캡슐화 작업을 거친 코드라고 할 수 있습니다. 새로운 객체가 필요하다면 위 생성자 함수를 다시 호출하면 됩니다. 따라서, 코드 전반적으로 반복을 줄여 주고 재사용성을 늘려주는 장점을 갖게 해 줍니다.  


### &nbsp;(2) Inheritance (상속)

&nbsp;'Inheritance (상속)'란, 부모 객체의 속성과 기능을 자식 객체가 물려받는 것입니다.  

&nbsp;자식 객체는 부모 객체의 속성/기능을 물려받으므로, 별도로 속성/기능을 매번 선언해 주지 않더라도 부모 객체의 그것을 갖고 있을 수 있습니다.  

&nbsp;물론, 자식 객체를 선언하거나 활용하면서, 기존의 속성/기능을 수정하거나 새로운 속성/기능을 부여해줄 수도 있습니다.  

&nbsp;상속 덕분에 복잡성을 줄일 수 있고, 일정한 변화를 주어야 할 때 그 변화를 더 쉽게 반영할 수 있습니다.  

&nbsp;상속의 구체적인 문법에 관하여 별도 글을 작성하려고 합니다. [링크 추가할 것!]();

### &nbsp;(3) Abstraction (추상화)

&nbsp;위에서 살폈듯이, 객체지향 프로그래밍은 주변의 실생활에서 볼 수 있는 것들을 객체 형태로 구현하여 프로그래밍에 사용할 수 있돌고 할 수 있습니다.  

&nbsp;그런데, 예를 들어 '노트북'이라는 어떤 존재를 객체로 작성하기 위해 이 노트북의 특징을 하나하나 객체 안에 반영한다면, 정말 많은 내용을 작성해야 할 것이고 이 모든것들이 실제로 프로그래밍에서 사용되지도 않을 것입니다.  

&nbsp;이런 경우 추상화를 통해, (사용자에게?) 필요하지 않은 부분은 삭제하거나 접근하지 않도록 할 수 있습니다. 가령 노트북이라면, '화면크기, 메모리 크기, 설치된 운영체제, 지원하는 수많은 기능들' 등 굉장히 많은 요소를 찾을 수 있습니다. 그리고 이런 각각의 다수 요소들을 모두 정의하기는 효율적이지 않습니다.   

&nbsp;그런데, 코드 안에서는 '색상, 가격, 주인이름' 정도의 간단한 사항들로 데이터의 종류를 한정하고, 프로그램 안에서는 이것들만을 활용할 필요가 생길 수 있습니다. 객체는 이러한 것을 실현할 수 있으며, 이런 특징을 'Abstraction (추상화)'라고 합니다.  

&nbsp;이런 특징 덕분에 보다 직관적으로 기능을 구현/사용할 수 있고, 프로그램에서 필요로 하도록 개발자가 의도한 그 내용에 한정해서 접근/사용할 수 있게 됩니다.  

&nbsp;OOP에서는 "Single Resposibility" 라는 개념이 있다고 합니다. '단 하나의 기능만을 하라' 라는 뜻으로 이해했습니다. 어떤 함수가 실행될 때 필요 이상으로 여러 기능을 수행할 수 있도록 함수를 구현한다면, 이는 직관적이지도 못하고 효율성도 떨어질 것입니다. 그러나, 이 함수가 가진 기능을 여러개로 나누어 구현한다면, 보다 간소화된 코드를 더 효율적으로 사용할 수 있을 것입니다.  

### &nbsp;(4) Polymorphism (다형성(?))

&nbsp;이는 "객체는 부품화시킬 수 있다"는 특징입니다.  

&nbsp;가령 '노트북'이라는 하나의 객체가 있다고 하고, 이 객체 안에는 '저장장치'라는 요소가 있다고 할 때, 이 저장장치에는 'HDD'라는 부품이 들어올 수도 있고, 'SSD'라는 부품 역시 들어올 수 있습니다.  

&nbsp;'저장장치'라는 기본 클래스 아래에서, 이를 상속받는 'HDD'라는 부품과 'SSD'라는 부품은, 같은 부모를 상속받았으므로 기본 틀은 동일하지만, 실제 세부 구현 과정에서는 다르게 구성되어 있다고 하겠습니다.    

&nbsp;이런 경우, '노트북' class로 만든 새로운 노트북 instance의 저장장치 부분에 어떤 저장장치 class를 활용할지에 따라서, 상위 instance인 노트북의 기능 또는 성능이 달라질 수 있게 됩니다.  

&nbsp;'다형성'은 "같은 타입이지만 실행 결과가 다양한 객체를 대입(이용)할 수 있는 성질"을 말합니다. 같은 '저장장치' 타입이지만, 'HDD'와 'SSD'는 실행 결과가 각자 다른 새로운 하위 객체입니다. 이렇게 서로 다른 객체가 대입될 수 있다는 특징이 '다형성' 입니다.

<!-- &nbsp;(다형성은 공부가 더 많이 필요함)
 -->
<br>
---
<br>

# 4. Instantiation Patterns  

&nbsp;'인스턴스'를 만드는 패턴에 관하여 알아보겠습니다.  

&nbsp;현재의 ES6 Javascript에서는 `class` 키워드가 존재하여 클래스를 표현하고 다룰 수 있게 되어 있습니다. (이에 관하여도 별도 정리하도록 하겠습니다.) 덕분에 Javascript는 한층더 객체지향적으로 활용할 수 있습니다.  

&nbsp;하지만, ES6 이전의 ES5에서도 Javascript를 객체지향적으로 다룰 필요성은 존재했습니다. 이는 `class` 키워드가 없는 ES5에서 class 기능을 구현하여 사용하기 위해, 이를 선언해 주기 위한 방식입니다.  

 - Class : 나중에 반복적으로 사용하기 위한 기본 틀을 만들어 두는 것으로써, 복사본을 위한 원본이 되는 기본 세팅/청사진이라고 생각할 수 있습니다.  
 - Instance : Class를 복사해서 만들어내는 새로운 객체이며, 실제 활용하기 위한 대상이 됩니다. Class에서 선언한 속성/기능 등을 매번 다시 선언해 주지 않더라도, Class에서 그대로 가져올 수 있게 구성되어야 합니다.  

&nbsp;특히 'Pseudoclassical(의사 클래스 방식, Pseudo Classical Method)' 방식에 관하여 다루겠습니다.  

### &nbsp;(1) Functional

&nbsp;함수의 구조를 활용하여 Class와 Instance를 구현하는 방식입니다.  

```javascript
let Coffee = function (nickname, temp, milk) {
  let someCoffee = {};

  someCoffee.nickame = nickname;

  someCoffee.temp = function () {
    if (temp === "ice") {
      return "ice";
    }
    if (temp === "hot") {
      return "hot";
    }
  };

  someCoffee.coffeeName = function () {
    let coffeeName = "";
    
    if (this.temp === "ice") {
      coffeeName = coffeeName + "ice" + " ";
    }
    if (this.temp === "hot") {
      coffeeName = coffeeName + "hot" + " ";
    }
    if (milk === true) {
      coffeeName = coffeeName + "cafe latte";
    }
    else {
      coffeeName = coffeeName + "cafe americano";
    }
    return coffeeName;
  };

  someCoffee.call = function () {
    return this.nickame + "!, your " + this.coffeeName() + " is ready!";
  };

  return someCoffee;
};

```  

&nbsp;가령 위와 같이 Class를 작성한 뒤,  

```javascript
let john = Coffee("john", "hot", false);
let jack = Coffee("jack", "ice", true);
```  

&nbsp;이렇게 class를 함수로 구현한 `Coffee` 함수를 활용하여 새로운 instance를 만들어내고,  

```js
john.call();  //  "john!, your cafe americano is ready!"
jack.call();  //  "jack!, your cafe latte is ready!"
```  

이런 방식으로 사용할 수 있게 됩니다.  


### &nbsp;(2) Functional Shared

&nbsp;위와 같이 하나의 Class 함수 안에서 한번에 모두 선언하지 않고, 초기에는 Class 함수의 껍데기만 선언합니다.  

&nbsp;이후, 그 Class 함수에서 활용할 Method들은, 함수 외부에서 별도로 선언한 뒤, 양 객체를 합칠 별도의 함수를 작성하고 Class 안에서 실행되도록 합니다.    

&nbsp;이렇게 하여, Method들을 외부에서 작성한 뒤 Class 안으로 반영할 수 있는 코드를 작성할 수 있습니다.  

&nbsp;위에서 작성한 코드를 이 방법으로 변경하려니 변수를 조정해야 하는 것 때문에 코드내용이 많이 변경되게 되었습니다. 그래서 이 부분은 다른 예시 코드를 작성하였습니다.  

```js
let mergeMethods = function (toMethod,fromMethod) {
  for (let key in fromMethod) {
    toMethod[key] = fromMethod;
  }
};

let methods = {};
methods.levelUp = function () {
  this.level += 1;
};
methods.levelDown = function () {
  this.level -= 1;
};

let Elevator = function (level) {
  let newInstance = {
    level : level
  };

  mergeMethods(newInstance, methods);

  return newInstance;

};    // 작동을 안하는데, 수정 필요
```  

&nbsp;Class 안에서 Method들 선언하지 않더라도, instance가 정상 생성되는 것을 볼 수 있습니다.  

&nbsp;'Functional' 방식은 매번 instance가 생성될때마다 메소드 역시 모두 새롭게 생성되므로 메모리를 더 많이 차지합니다. 그러나 Functional Shared 방식은 메소드를 새로 생성하지 않고 단지 참조하므로, 메모리 면에서 훨씬 유리합니다.   

### &nbsp;(3) Prototypal

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/create

```js
    // 예시 코드 작성헤야 함
    // JavaScript에서 Prototype은 무엇이고 왜 사용해야 하는지?
```

### &nbsp;(4) Pseudoclassical (의사코드?)

```js
let Elevator = function (level) {
  this.level = level;
};

Elevator.prototype.up = function () {
  this.level += 1;
};
Elevator.prototype.down = function () {
  this.level -= 1;
};

let elevator1 = new Elevator(3);
let elevator2 = new Elevator(8);

elevator1.up();
elevator1.up();
elevator2.down();
elevator2.down();

elevator1.level;  // 5
elevator2.level;  // 6
```  

&nbsp;가장 많이 쓰이는 방법입니다. instance 선언시에 꼭 `new`를 붙여줘야 합니다.  

---  

<br>
---
<br>

&nbsp;이와 같이, 객체지향 프로그래밍에 관한 공부를 시작해 보았습니다.  

&nbsp;위 내용은 이제 막 시작한 것에 불과하며, 이마저도 보완할 점이 많으므로, 계속 수정해서 더 좋은 글로 다듬도록 하겠습니다.  