---
title: 'JavaScript ES6 문법 공부'
excerpt: 'Arrow Function / let & const / Default Parameter Values / Function Rest Parameter'

categories:
  - studynote
tags:
  - javascript
  - ES6
last_modified_at: 2021-01-26
---

`ES6`는 `ECMAScript 6`의 다른 표현입니다.

`JavaScript`를 표준화하기 위해 만들어진 기술 규격 `ECMAScript`의 6번째 버전이며, 2015년에 발표되었으므로 `ECMAScript 2015`라고도 합니다. 2019년 발표된 `ES10 / ES2019`가 최신 버전입니다.

[w3school의 문서](https://www.w3schools.com/react/react_ES6.asp)에 따르면 `React`는 `ES6`를 사용한다고 합니다. `React`를 잘 사용하는 것은 중요하므로 `ES6`의 문법에 꼭 익숙해져야 하겠습니다. 따라서 아래에서는 `ES6`에 추가된 사항 중 일부에 관해서 정리하였습니다.

---

# `Arrow Function`

`Arrow Function` 문법은 함수를 보다 쉽게 작성할 수 있도록 개선된 문법입니다.

기존에 사용되었던 함수 작성 방식은,

- `function` 이라는 명칭을 붙여야 하고,
- `return` 역시 필요했으며,
- `curly brackets`(`{`, `}`) 도 필요했습니다.

```js
// ES5
function sum(a, b) {
  return a + b;
}
```

그러나, Arrow Function 문법을 사용하면 아래와 같이 단순화하여 작성할 수 있습니다.

```js
// ES6
const sum = (a, b) => a + b;
```

`Arrow Function` 문법을 사용할 때에는 아래와 같은 사항을 지켜야 합니다.

- `this`의 사용법이 다릅니다. 기존 함수에서는 기본적으로 `window`와 같은 전역 객체를 가리키고, `bind`(`ES5`에서 도입되었습니다.)를 통해 특정 객체를 가리키게 할 수 있습니다. 그러나 `Arrow Function`에서 `this`는 자신이 포함된 정적 범위(lexical context)입니다. (전역 코드에서는 전역 객체입니다.) `Arrow Function`은 `bind`되지 않습니다.
- `Arrow Function`은 `호이스팅(hoist)`되지 않습니다. 따라서 함수가 사용되기 전 단계에서 필히 먼저 선언되어야 합니다.
- `Arrow Function`은 그 함수가 한 줄로 끝나는 경우 이를 `return` 값으로 인식합니다. 그렇지 않고 함수에 여러 줄이 나열된다면 `return / curly brackets`을 꼭 사용해야 합니다.

---

# `let` / `const`

기존 `ES5`에서는 변수 선언시 `var`라는 방식을 활용했습니다. 이후 `ES6`에서는 `let`이라는 새로운 방식으로 변수를 선언할 수 있게 되었습니다.

둘 사이의 차이는 다음과 같습니다.

(1) `var`는 `function scope`를 갖습니다.

- 함수 밖에서 변수를 선언하면, 이는 전역 객체에 속하게 됩니다.
- 함수 안에서 변수를 선언하면, 이는 함수 안에 속하게 됩니다.
- (반복문 등과 같은) 일정한 블록 안에서 변수를 선언하면, 이 변수는 해당 블록 밖에서도 접근할 수 있게 됩니다.

(2) `let`은 `block scope`를 갖습니다.

- 기본적으로 `var`와 동일한 성격을 갖습니다.
- 다만, 블록 안에서 변수를 선언할 경우에는, 해당 블록 안에서만 이 변수에 접근할 수 있고 그 밖에서는 접근이 불가능합니다.

이러한 차이 덕분에, `block scope` 안에서 일정한 변수를 선언한 뒤 밖에서 같은 이름의 변수를 사용하는 경우,

- `var`는 `block scope` 외부에서도 그 안에 있는 값에 접근할 수 있으나,
- `let`은 `block scope`가 끝나면서 변수 참조가 사라졌으므로 새로운 변수로 인식하고 (선언되지 않은 값에 접근하려는 시도이므로) 에러를 반환하게 됩니다.

```js
{
  var a = 1;
  let b = 2;
  console.log(a); // 1
  console.log(b); // 2
}

console.log(a); // 1
console.log(b); // Uncaught ReferenceError: b is not defined
```

이런 성질 덕분에 변수 선언/사용에서 혼동을 줄일 수 있어서, 저는 변수 선언시에 `let`을 사용하고 있습니다.

이와 함께, 값의 재선언에서 오는 문제점을 막기 위해 `const`라는 문법이 추가되었습니다.

`let`은 '변수'이므로, 그에 담긴 값이 변화할 수 있습니다.

```js
let a = 1;
console.log(a); // 1

a = 'apple';
console.log(a); // 'apple'
```

`let`은 변수이므로 이런 방식으로 같은 이름의 값에 새로운 내용을 다시 할당할 수 있어서, 코드 작성 과정에서 어떤 실수로 값을 재할당하면 실행 과정에서 문제가 남게 됩니다.

- 물론, `let` 역시 같은 이름으로 `let`을 붙여 아래와 같이 선언하면 이미 선언되었다는 에러가 나오게 됩니다. (`Uncaught SyntaxError: Identifier 'a' has already been declared`)

이런 점을 방지하기 위해, 어떤 값들은 변수가 아닌 상수로 선언하고 그 이후에는 값의 변화를 막을 필요가 있게 되었고 이를 위해 만들어진 문법이 `const` 입니다.

```js
const a = 1;
console.log(a); // 1

a = 'apple';
console.log(a); // Uncaught TypeError: Assignment to constant variable
```

---

# `Default Parameter Values`

`ES6`에서는 함수의 선언에서 그 매개변수에 일정한 기본값을 설정할 수 있습니다.

```js
const sum = (a, b) => a + b;
```

위와 같은 함수가 주어졌을 때,

- `sum(1, 2);` 이렇게 작성한다면 '3'이라는 결과를 얻을 수 있습니다.
- 그러나, `sum(1);` 이렇게 작성한다면, 매개변수 `a`는 '1'로 주어졌으나 `b`는 그 값이 주어지지 않아 `undefined`가 됩니다. 연산 결과는 `NaN`이 됩니다.

필요에 따라서는 어떤 매개변수는 상황에 따라 주어지거나 주어지지 않을 것을 필요로 할 수도 있습니다. 이 경우, 각 매개변수마다 '그에 대응하는 값이 주어지지 않는 경우, 해당 매개변수가 가질 기본값'을 설정할 수 있는 문법이 `Default Parameter Values` 입니다.

```js
const sum = (a, b = 10) => a + b;

sum(1, 2); // 3
sum(1); // 11
```

저는 이 문법을 `Redux`의 `reducer 함수`에서 사용했습니다.

- `Redux Store` 안의 '기본값'이 될 `initialState` 객체를 선언합니다.
- 이를 변경하기 위한 `reducer 함수`의 두 매개변수 중, 첫번째 매개변수에 이 `initialState` 객체를 '기본값'으로 할당합니다.

```js
// initialState (아래에서 사용될 기본값)
const initialState = {
  login: {
    status: 'INIT',
  },
  status: {
    isLoggedIn: false,
    currentUser: null,
    nickname: null,
  },
};

// `reducer 함수` (`Default Parameter Values` 사용)
// 매개변수 `state`에 기본값 `initialState` 할당
export default function loginOut(state = initialState, action) {
  switch (action.type) {
    case AUTH_LOGIN_START:
      return {
        ...state,
        login: {
          ...state.login,
          status: 'WAITING',
        },
      };

    ... // 중간 생략

    default:
      return state;
  }
}

```

---

# `Function Rest Parameter`

함수가 몇 개의 매개변수를 받는지가 고정되어 있지 않을 수 있습니다.

- 가령 `sum()` 이라는 함수는, 매개변수로 주어지는 모든 값들 중 숫자만을 더한 값을 출력하기를 원한다고 할 수 있습니다.

이런 경우, `ES6` 이전에는 `arguments`라는 특수한 객체를 활용해서 함수에 주어지는 모든 매개변수를 담을 수 있었습니다.

```js
function sum() {
  let answer = 0;
  for (let i = 0; i < arguments.length; i++) {
    if (typeof arguments[i] === 'number') {
      answer += arguments[i];
    }
  }
  return answer;
}

sum(1, 2, 3); // 6
sum(1, 2, 3, 4); // 10
```

그러나, `arguments` 객체는 실제 배열이 아니라 `유사배열객체(array-like object)`이므로,

- `length`값이 존재하고 순회가 가능하지만,
- 배열이 아니므로 `forEach`, `map`, `filter` 등의 배열 기본 메소드를 활용할 수 없습니다.

그래서, 함수의 매개변수를 실제의 배열 형태로 받아올 필요에 대응하기 위해, `Rest Parameter`를 함수의 매개변수에도 활용할 수 있게 되었습니다.

```js
function sum(...args) {
  let answer = 0;
  for (let i = 0; i < args.length; i++) {
    if (typeof args[i] === 'number') {
      answer += args[i];
    }
  }
  return answer;
}

sum(1, 2, 3); // 6
sum(1, 2, 3, 4); // 10
```

위 코드에서 `args`는 유사배열객체가 아닌 실제 배열이므로, 이 함수는 아래와 같이 변경할 수 있습니다.

```js
function sum(...args) {
  return args.reduce((acc, cur) => {
    if (typeof cur === 'number') {
      return acc + cur;
    }
  }, 0);
}

sum(1, 2, 3); // 6
sum(1, 2, 3, 4); // 10
```

`arguments`와는 달리, 배열의 기본 메소드 `reduce`를 활용할 수 있습니다.

- `arguments`를 활용한 같은 코드는 `Uncaught TypeError: arguments.reduce is not a function` 이라는 결과를 보여주게 됩니다.

---

# `Destructuring Assignment(구조분해 할당 or 비구조화 할당)`

기존 `JavaScript`에서는 객체의 각 값을 변수에 할당하려면 아래와 같이 작성했습니다.

```js
let obj = {
  a: 1,
  b: 2,
};

let a = obj.a; // 1
let b = obj.b; // 2
```

이 코드를 `Destructuring Assignment`를 활용하면 보다 간단하게 표현할 수 있습니다.

```js
let { a, b } = obj;

concole.log(a); // 1
concole.log(b); // 2
```

이런 방식은 `React`의 모듈을 불러올 때에도 활용하고, `Redux`의 `state`를 불러올 때에도 활용할 수 있습니다.

- 다른 위치에서 `export { MainPage };` 형태로 모듈을 내보내는 경우, 이를 가져올 때에는 `import { MainPage } from './***';` 이러한 방식을 취하게 됩니다.
- 위에서 예시로 든 `Redux`의 `initialState` 객체에서, 이 객체 전부를 다 불러오지 않고 `currentUser` 값만을 불러오는 경우, `const { currentUser } = useSelector((state: RootState) => state.loginOut.status);` 이렇게 작성하게 됩니다.

`Destructuring Assignment` 문법은 객체 뿐만 아니라 배열에서도 활용할 수 있습니다.

- `React`의 `useState` `Hook`을 활용할 때, `const [newNickname, setNewNickname] = useState('');` 이렇게 작성하여 각 값을 활용하게 됩니다.
- 배열 안에서 어떤 두 값의 위치를 서로 바꿔줘야 할 때, `[b, a] = [a, b];` 이런 방식으로 결과를 얻을 수 있습니다.
- 어떤 배열(`const arr = [1, 2, 3, 4, 5];`)에서 일정 범위의 필요한 값들만을 가진 새로운 배열을 만들어야 할 때, `let [x, y, ...rest] = arr;` 이렇게 작성한다면 각각의 이름으로 배열 안의 요소들을 나누어 넣어줄 수 있습니다.

---

코드를 작성하면서 가능하다면 `ES6` 문법을 활용하려고 합니다. 앞으로도 더 공부하고 실제로 활용하게 되는 문법들을 이 글에 이어서 적어두겠습니다.
