---
title:  "call by value 와 call by reference 비교하기 - 데이터 참조의 구조"
excerpt: "\"인자와 매개변수 사이의 관계 - 매개변수는 무엇을 가리키는가?\""

categories:
  - studynote
tags:
  - Javascript
  - memory
  - call by value
  - call by reference
last_modified_at: 2020-04-05
---


<br>

# 들어가면서,  

&nbsp;과제를 위해 코드를 작성하던 중, 아무리 봐도 제대로 작성한 것 같은데 의도했던 결과값이 나오지 않아 당황했던 적이 있습니다.  

&nbsp;친구의 조언에 따라 문제는 해결했었고 원하는 결과를 볼 수 있었는데,  

>'지금 생긴 문제는 call by value 와 call by reference 의 차이 때문에 생긴 문제이니, 이 부분을 나중에라도 꼭 공부하라'  

&nbsp;라는 친구의 조언을 공책 한쪽에 적어 두었습니다.  

&nbsp;어느 과제에서 어떤 코드가 문제가 되었는지를 기록하여 남겨두었다면 좋았을텐데 참 아쉽습니다.  

&nbsp;그래도 개발 공부에 중요한 부분이라는 생각에 공부하였으며, 그 기록을 이 포스트에 남겨두고 나중에 또 복습하도록 하겠습니다.  

<br>




# 데이터 타입 (자료형)  

&nbsp;먼저 데이터 타입을 짚고 넘어가겠습니다.
 1. Primitive Type  
 &nbsp;`number`, `string`, `boolean`, `undefined`, `null` 등이 이에 속합니다.  
 &nbsp;이 값들은 더이상 단순화할 수 없어 원시적(primitive)이라고 하며, 자바스크립트에서 활용할 수 있는 가장 단순한 형태의 데이터입니다.  
 &nbsp;따라서, 이러한 원시 타입의 데이터는 이를 만들기 위해 생성자 함수나 new 연산자 등이 필요하지 않습니다.  

 2. Reference Type  
 &nbsp;`Array`, `Object`, `function` 등이 이에 속합니다.   
 &nbsp;배열, 객체, 함수 등으로 예시를 나열하였으나, 이 모두는 사실 객체의 한 종류입니다.  
 &nbsp;내장 생성자 함수(`Object()`, `new` 등)를 이용해서 객체를 생성합니다.  


<br>  





# 복사와 참조    

## I. Primitive Type 데이터의 값은 '복사'됩니다.  

```js
let a = 3;
let b = a;
console.log(a);         // 처리하기 전의 a의 값은 3 입니다.
console.log(b);         // 처리하기 전의 b의 값은 3 입니다.
a = 10;                 // a에 새롭게 10을 넣어줍니다.
console.log(a);         // 처리 후 a의 값은 변경되어 10 입니다.
console.log(b);         // 처리 후 b의 값은 여전히 3 입니다.
```

&nbsp;원시 자료형은 변하지 않습니다.  
&nbsp;그러므로 원시값을 교체할 수는 있지만, 직접 변형할 수는 없습니다.  
>원시 타입의 데이터는 변수에 할당이 될 때 메모리 상에 고정된 크기로 저장이 되고 해당 변수가 원시 데이터 값을 보관한다.  
>원시 타입 자료형은 모두 변수 선언, 초기화, 할당 시 값이 저장된 메모리 영역에 직접적으로 접근한다.  
>즉, 변수에 새 값이 할당이 될 경우, 변수에 할당된 메모리 블럭에 저장된 값을 바로 변경한다.  
>(인용 : [JavaScript - Primitive Type(원시 타입) vs Reference Type (참조 타입)에 대해 알아보자](https://velog.io/@surim014/JavaScript-Primitive-Type-vs-Reference-Type))  

## II. Reference Type 데이터의 값은 '참조'됩니다.   

```js
// 배열 메소드는 배열을 변형함
var foo = [];
console.log(foo);        // 처리하기 전에 foo 의 값은 [] 입니다.
foo.push("plugh");       // .push 처리를 거치면, foo 의 값 [] 에 직접 변화를 주게 됩니다.
console.log(foo);        // 그러므로, 배열 foo 는 .push 처리를 거치면 ["plugh"] 로 변경됩니다.
```  
&nbsp;  
&nbsp;원시 타입은 '값 그 자체를 복사한 새로운 값'으로 전달되지만, 참조 타입은 '값이 존재하는 장소'(메모리 주소)를 전달합니다.  
&nbsp;  

```js
const origin = { a: 1, b: 2, c: 3, d: { q:1, w:2, e:3, }, } 

const copy = origin; 

copy.b = 1000; 

console.log(origin.b); // result 1000
```
&nbsp;위 예제에서, copy에 할당된것은 origin의 메모리 주소입니다.  
&nbsp;그로 인해, copy의 값을 바꿨지만 사실은 origin의 메모리 주소에 들어있는 값을 바꾼 것이므로, origin의 값도 변경됩니다.  
&nbsp;(출처: [[ JavaScript ] 원시타입(primitive type)과 참조타입(reference type)](https://ryulog.tistory.com/140))

<br>  




# call by value  
&nbsp;아래 예제를 살펴보겠습니다.  
```js
let x = 5;

function getTripledNumber (y) {
  y = y * 3;
}

getTripledNumber(x);

console.log(x);         // 5
```
&nbsp;위 예제에서, `x` 는 `getTripledNumber` 함수에서 처리되면서, 스스로에 3배 곱해진 값을 `x` 에 대입하게 됩니다.  
&nbsp;함수 안에서 `console.log(y)` 처리한다면, 이는 15가 표시될 것입니다.  
&nbsp;그러나, 함수가 종료된 뒤 `x` 값을 다시 표시하면 이는 여전히 5 입니다.  
  
&nbsp;이는 위 예제의 `x` 를 `getTripledNumber` 함수에 넘겨줄 때, 그 값을 그냥 넘겨주는 것이 아니라, 이를 '복사'하여 넘겨주기 때문입니다.  
`getTripledNumber` 함수 안에서는 `x` 를 가지고 처리한 것이 아니라, `x` 의 값인 `5` 를 '복사'해서 함수로 넘겨주므로 함수에서는 이 복사된 값을 가지고 일정한 처리를 하게 되는 것입니다.  
  
&nbsp;함수의 인자로 Primitive Type 값이 전달되면, 함수에서는 전달받은 인자를 '새로운 주소에 복사'한 뒤 이 새로운 값으로 처리합니다.  
&nbsp;인자가 복사되었으므로, 전달된 인자(원래의 인자)와 전달받은 인자(함수 안에서 복사되어 새롭게 생긴 인자)는 전혀 다른 값(주소값이 다름)이 됩니다.  
&nbsp;따라서 함수 등의 '일정한 처리를 거친 뒤에도, 값이 변경되지 않습니다'.  

<br>  




# call by reference  
&nbsp;아래 예제를 살펴보겠습니다.  
```js
let x = { name : "jack", car : "Avante" };

let y = x;

console.log(y)  // { name : "jack", car : "Avante" } 출력
```  
 &nbsp;위 예제에서, `let x = { name : "jack", car : "Avante" };` 코드를 해석하면,  
  - 변수 x 안에 `{ name : "jack", car : "Avante" }` 값이 들어있는 것이 아니라,
  - 변수 x 안에는 `{ name : "jack", car : "Avante" }` 의 '주소(메모리 위치)'를 가리키고 있다고 보아야 합니다.  
   
 &nbsp;`let y = x;` 코드를 해석하면,  
  - 변수 y 안에 변수 x의 `{ name : "jack", car : "Avante" }` 값이 들어있는 것이 아니라,  
  - 변수 y 는 변수 x 가 가리키는 `{ name : "jack", car : "Avante" }`의 '주소(메모리 위치)'를 가리키고 있다고 보아야 합니다.  
&nbsp;  
  
&nbsp;여기에서 다음과 같은 결론을 내릴 수 있습니다.  
  - "Reference Type 데이터를 넘겨 주면, 그 값의 복사된 데이터가 아닌, 그 값의 주소를 참조한다."
  - "따라서, 함수 등의 안에서 Reference Type 데이터에 변경을 가하면, 그 주소를 참조하여 원래의 Reference Type 데이터 역시 변경될 수 있으므로, 주의를 기울여야 한다."  
  - 결론적으로, "함수의 매개변수가 원시타입(Primitive Type)인 경우에는 Call By Value 고, 매개변수가 객체형태면 Call By Reference 로 동작한다."  
  
    그런데, **다음의 사례를 보면 상황이 달라집니다.**  

<br>  




# call by sharing  
&nbsp;아래 예제를 살펴보겠습니다.  
&nbsp;(이하 출처 : [[javascript] call by value](https://blueshw.github.io/2018/09/15/pass-by-reference/))  
&nbsp;(참고 : call by sharing 이라는 표현은 정규 용어는 아니라고 합니다.)  
  
### 재할당(Reassigning of Reference Type)  
  
```js
let obj = { p1: 10 }
let objCopy = obj
console.log(obj === objCopy) // true

objCopy = { p2: 100 }
console.log(obj === objCopy) // false
```  
&nbsp;위 코드에서, 먼저 선언된 `obj`와 이후에 선언된 `objCopy`는 같은 객체 `{ p1: 10 }`의 '주소를 참조하고(가리키고)' 있습니다.  
&nbsp;이 시점에서는 `obj`와 `objCopy`를 비교하면, 같은 주소를 참조하므로 `true`가 출력됩니다.  
  
&nbsp;그러므로, 이후 `objCopy`에 `{ p2: 100 }`가 '재할당'되면, `objCopy`는 이제 새로운 객체 `{ p2: 100 }`의 '새로운 주소를 참조하게' 됩니다.  
&nbsp;그러므로 두 변수를 비교하면, 이제는 각자 다른 주소를 참조하므로 `false`가 출력됩니다.  
  
### Reference Type 데이터인 인자를, 함수내에서 변경(속성만 변경)하면 어떻게 될까?  


```js
let foo = [];
let bar = foo;

console.log(foo);       // 처리 전의 foo 는 [] 입니다.
console.log(bar);       // 처리 전의 bar 는 [] 입니다.

foo.push("plugh");      // foo에만 "plugh" 문자열을 push 합니다.

console.log(foo);       // 처리 후의 foo 는 ["plugh"] 입니다.
console.log(bar);       // 처리 전의 bar 는 ["plugh"] 입니다.
```  
&nbsp;위 코드에서, `foo`는 `[]`의 주소를 참조하고(가리키고) 있습니다.  
  
&nbsp;`bar` 변수는 `foo` 변수가 참조하는 주소를 복사하여 참조합니다.  
  
&nbsp;`foo` 배열에 `.push` 메소드로 `"plugh"` 문자열을 `.push`하면, `foo` 변수는 여전히 같은 주소를 가리키지만, 그 주소의 값인 `[]`에는 위 처리에 의한 변경이 반영됩니다.  
  
&nbsp;이 처리 과정에서 `bar`에는 변경이 가해지지 않았습니다. 그럼에도 불구하고, `bar` 역시 `foo`와 같은 주소를 참조하고 있으며 '그 주소에 존재하는 값 `[]`에 변경이 가해졌으므로', `bar` 역시 위 처리에 의한 변경이 반영됩니다.
  
&nbsp;그러므로 참조되고 있는 `[]`의 값 자체가 변경되어, 함수 처리가 종료된 뒤 이 값의 주소를 참조하고 있던 두 변수 모두 변경된 값 `["plugh"]` 형태가 출력되게 됩니다.  
  
### Reference Type 데이터인 인자를, 함수내에서 변경(새롭게 재할당)하면 어떻게 될까?  
```js
const o = { p1: 1 }
function change(obj) {
  obj = { p1: 100 }
}
change(o)
console.log(o)      // 처리를 거쳤음에도 변경되지 않고 {p1: 1} 로 출력됩니다.
```  
&nbsp;위 코드에서, `o`는 이번에도 `{ p1: 1 }`의 주소를 참조하고(가리키고) 있습니다.  
  
&nbsp;`change()` 함수에 `o`가 인자로 전달되면, `obj`는 `o`를 복사한 객체이므로 `{ p1: 1 }`의 주소를 참조하게 됩니다.  
  
&nbsp;`change()` 함수에 전달된 `obj`에 `obj = { p1: 100 }` 처리를 가하면, `obj`는 더이상 `{ p1: 1 }`의 주소를 참조하지 않고, 새롭게 생성된 `{ p1: 100 }`의 주소를 참조합니다.  
  
&nbsp;따라서, 이 처리 과정에서 `obj`가 참조하는 객체의 주소가 `{ p1: 100 }`의 주소로 변경되었습니다.  
  
&nbsp;그러므로 참조되고 있는 `{ p1: 1 }`의 값에 변경을 가하지 않았으며, 함수 처리가 종료된 뒤 `o`를 확인하면 함수 안에서 재할당(대입)된 `{ p1: 100 }`가 아닌 `{ p1: 1 }`가 출력되게 됩니다.  

<br>  




# 정리 - JavaScript 에서는 `call by value` 로 동작한다.

&nbsp;위 사례들에서 보다시피, Reference Type 데이터를 인자로 전달하더라도, 함수 안에서 '매개변수의 속성을 변경하는지' 또는 '매개변수 자체를 재할당하는지'에 따라서, 결과가 달라지는 것을 볼 수 있습니다.  
  
&nbsp;이는 Reference Type 데이터인 인자가 전달된다면 그 데이터 자체가 아닌 그 데이터의 '주소값'이 전달되기 때문입니다.  
  
&nbsp;그래서, 함수 안에서 매개변수의 '속성을 변경'하면,  
 - Primitive Type 데이터의 '값이 복사'되는 것처럼, '인자의 주소값'이 전달되고,  
 - 최초 전달된 데이터의 주소값은 전달된 뒤 함수 안에서도 여전히 같고 그 속성만을 변경하므로,  
 - 같은 주소에 처리를 가한 것이 되어, 함수종료 후에 인자를 확인하면 **처음에 전달된 인자의 값 자체가 변경되게 됩니다**.  
  
&nbsp;그리고, 함수 안에서 매개변수를 '재할당'하면,  
 - Primitive Type 데이터의 '값이 복사'되는 것처럼, '인자의 주소값'이 전달되고,  
 - '최초 전달된 주소값'과 '새롭게 재할당된 뒤의 주소값'이 서로 달라지므로,  
 - 서로 다른 주소에 처리를 가한 것이 되므로, 함수가 종료된 뒤에도 **처음에 전달된 인자는 변경되지 않고 유지됩니다**.  
  
<br>  
&nbsp;그러므로, **<u>JavaScript 에서는, Reference Type 데이터를 인자로 전달하더라도, `call by reference` 와 같이 동작하지 않고 `call by value` 로 동작한다는 결론을 낼 수 있습니다.</u>**  

<br>  




# 작성후기 및 참조  
 - 이 포스트를 작성하면서, 아래와 같은 좋은 글을 많이 참조하였습니다.  
     - [자바스크립트의 자료형](https://developer.mozilla.org/ko/docs/Web/JavaScript/Data_structures)  
     - [원시값](https://developer.mozilla.org/ko/docs/Glossary/Primitive)  
     - [자바스크립트 function - Call by Value, Call by Reference](https://emflant.tistory.com/64)  
     - [자바스크립트 기본타입(원시값=단순값)](https://webclub.tistory.com/240)
     - [JavaScript - Primitive Type(원시 타입) vs Reference Type (참조 타입)에 대해 알아보자](https://velog.io/@surim014/JavaScript-Primitive-Type-vs-Reference-Type)
     - [[ JavaScript ] 원시타입(primitive type)과 참조타입(reference type)](https://ryulog.tistory.com/140)  
     - [10. 자바스크립트 : 원시 타입과 참조 타입](https://m.blog.naver.com/PostView.nhn?blogId=gi_balja&logNo=221137914754&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F)
     - [[javascript] call by value](https://blueshw.github.io/2018/09/15/pass-by-reference/)  
     - Learning JaverScript (이선 브라운 지음, 한선용 옮김, 한빛미디어)  
 - 이번 포스팅 역시 제가 창작하여 작성했다기보다는 다른 분들께서 정리해 주신 내용을 많이 가져다가 옮겨 작성하게 되었습니다. 작성자분들께 허락을 구하지 않고 내용을 참조하는 점 양해를 부탁드리며, 이 부분을 지적해 주신다면 언제든 삭제/수정하도록 하겠습니다.  
 - 서두에도 적었지만, 제가 실제로 마주한 난제를 가지고 포스팅을 할 수 있었다면 정말 좋았겠다는 생각이 듭니다. 앞으로는 무엇인가 문제가 생겼을 때, `그 문제 자체` / `시도한 방법들` / `그 해결방법` / `그 과정에서 배운 새로운 내용들` 등을 모두 기록해 두도록 노력하겠습니다. 이번 포스팅에서 배운 여러가지 중 하나는 이것입니다.  
 - 작성한 내용에 오류가 있거나 수정/보완할 내용이 있다면 지적해 주시면 정말 감사하겠습니다.  
 - 읽어주셔서 감사합니다.