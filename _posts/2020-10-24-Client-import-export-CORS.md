---
title: "첫 프로젝트 - Signup"
excerpt: "React Hook // export VS export default  //  CORS error"

categories:
  - First Project
tags:
  - Javascript
  - First Project
  - Frontend
last_modified_at: 2020-10-24
---

&nbsp;SR을 마무리한 뒤, 클라이언트 측에서는 일단 간단하게라도 mock-up을 만들어본 뒤 이어서 기능을 구현하기로 하였습니다.

&nbsp;그러나, 클라이언트를 담당한 (저를 포함한) 2명 모두 CSS에 부족함이 너무 많았고, 새롭게 접한 bootstrap은 공부할 것이 생각보다 너무 많았습니다.

&nbsp;그래서, 간단하게 형태만 잡아놓은 단계에서, 일단 기능부터 구현한 뒤 디자인을 수정해 나가자는 쪽으로 방향을 변경하였습니다.

---

<br>
<br>

## 1. 회원가입 기능 작성

&nbsp;그 뒤 처음으로 시작한 기능은 Signup(회원가입) 이었습니다.

&nbsp;앱의 첫 시작은 이용자가 글을 쓰기 위해 회원가입을 하는 것부터 시작하기 때문입니다.

&nbsp;이를 위해 서버 측에서 데이터베이스를 구축해 주셨고, 회원가입 기능에 맞는 코드를 작성하시어 API를 제공해 주셨습니다. 그래서 이에 따라 코드를 작성했습니다.

<br>
<br>

## 2. react hook

&nbsp;Redux를 활용하고 싶었지만, 일단은 Redux 코드 구현에 앞서, Fuctional Component를 사용하는 것이 더 좋다(?)는 말씀을 들어서, 이번에는 Fuctional Component로 코드를 작성해 보기로 했습니다.

&nbsp;Fuctional Component에서는 `state = {}` 이런 방식으로 상태를 관리할 수 없기 때문에, 상태 값을 활용하기 위한 방법으로 React Hook을 짧게 찾아 보았습니다.

&nbsp;아래와 같이 작성하였습니다.

```js
export default function Signup(props) {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [passwordConfirm, setPasswordConfirm] = useState("");

  function handleChange(e) {
    switch (e.target.name) {
      case "email":
        setEmail(e.target.value);
      case "password":
        setPassword(e.target.value);
      case "passwordConfirm":
        setPasswordConfirm(e.target.value);
      default:
        return;
    }
  }

  ...

  return (
    // 이 안에서는 email, password, passwordConfirm 3개의 입력 창을 주고,
    // 각 값이 바뀔때마다 `handleChange` 함수에서 상태값을 변경하도록 처리했습니다.

    ...
  )
}
```

&nbsp;React Hook의 여러 기능이 있지만, 그 중 간단하게 입력값을 받아 수정해 나가는 `useState()`를 활용해 보았습니다.

&nbsp;이후 더 진행해 나가면서, 필요한 기능들을 공부하여 적용해 보겠습니다.

<br>
<br>

## 3. Redux 코드 적용

&nbsp;상태 관리를 위한 Redux를 적용해서 앱을 구성하고 싶었습니다.

&nbsp;사실 앱의 크기가 작다면 Redux를 활용하지 않는 편이 오히려 코드 구성에 유리할 수도 있겠지만, 나중에는 Redux를 많이 쓰게 될 것이라는 생각에 연습해 두고 싶어서 적용을 시도했습니다.

&nbsp;스프린트에서 Redux를 다룬 경험이 있었지만, 사실 구조를 많이 이해하기는 어려웠습니다. 기본적인 이해가 상당히 부족한 상태여서, 이전에 혼자 진행했던 다른 튜토리얼 코드를 참고하여 `actions / components / containers / reducers` 등의 폴더 구조와 그 안의 세부 코드를 작성하였습니다.

&nbsp;그런데, 나름 코드를 작성한 뒤 `npm start` 명령어를 입력했는데, 아래와 같은 에러가 발생하였습니다.

![96751660-6dd68000-1408-11eb-956d-6b002ed344c5](https://user-images.githubusercontent.com/47794257/97034122-5d0c4280-159f-11eb-8595-dfec4b84a3f3.png)

![96907892-d2601080-14d6-11eb-9555-57792fb527cb](https://user-images.githubusercontent.com/47794257/97034144-65647d80-159f-11eb-8085-84c5c8e5af54.png)

![96907902-d7bd5b00-14d6-11eb-99e7-f11fbd5838b2](https://user-images.githubusercontent.com/47794257/97034161-6d242200-159f-11eb-82bd-1c76f9a5aa9e.png)

&nbsp;저는 이 에러가 나오는 이유가, 제가 Redux를 적용하면서 뭔가 잘못 쓴 것이 있다고 생각하고 한참에 걸쳐서 이렇게저렇게 수정했는데, 계속 같은 에러가 발생했습니다.

&nbsp;그래서 팀원 분께 도움을 청하여, Component를 내보내고 불러올 때 `export`와 `export default`의 차이 때문에 이 문제가 생겼음을 알 수 있었습니다.

[참고자료(MDN) : export](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/export)

[참고자료(MDN) : import](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/import)

&nbsp;'내보내기'에는 두 종류, 유명(named)과 기본(default) 내보내기가 있습니다. 모듈 하나에서, 유명 내보내기는 여러 개 존재할 수 있지만 기본 내보내기는 하나만 가능합니다. 각 종류는 위의 구문 중 하나와 대응합니다.

```js
/* 유명(named) 내보내기 */

// 먼저 선언한 식별자 내보내기
export { myFunction, myVariable };

// 각각의 식별자 내보내기
// (변수, 상수, 함수, 클래스)
export let myVariable = Math.sqrt(2);
export function myFunction() { ... };

/* 기본(default) 내보내기 */

// 먼저 선언한 식별자 내보내기
export { myFunction as default };

// 각각의 식별자 내보내기
export default function () { ... };
export default class { ... }
```

&nbsp;저는 Component를 내보내고 불러올 때, `export default { Signup };` 형태로 내보내고 `import Signup from "../components";` 형태로 불러오도록 코드를 작성했었습니다.

&nbsp;이렇게 작성하니 위의 에러가 반환되었는데, 이를 `export { Signup };` 형태로 내보내고 `import { Signup } from "../components";` 형태로 불러오도록 수정하니, 에러가 해결되었습니다.

&nbsp;`export default { Signup };` 형태로 작성하고 싶다면, import 위치에서 `import components from "../components";` 이런 방식으로 이름(가령 위의 components)을 붙여 받아온 뒤, 실제 이를 사용할 부분에서 `<components.Signup />` 이러한 방식으로 작성해야 에러가 없었습니다.

&nbsp;`export`와 `export default`, 그리고 `import` 등의 문법을 다시 볼 수 있는 기회가 되었습니다.

<br>
<br>

## 4. CORS 에러

&nbsp;저는 서버에 (회원가입을 위한) post 요청을 하는 부분을 아래와 같이 작성한 상태입니다.

```js
/* REGISTER */
export function registerRequest(email, password) {
  return (dispatch) => {
    // Inform Register API is starting
    dispatch(register());

    return axios
      .post(
        "http://localhost:5000/users/signup",
        { email, password },
        { withCredentials: true }
      )
      .then((response) => {
        dispatch(registerSuccess());
      })
      .catch((error) => {
        dispatch(registerFailure(error.response));
      });
  };
}

// 이하에 있는 액션생성자 함수들은 생략하였습니다.
// register(), registerSuccess(), registerFailure()
```

&nbsp;저는 위 내용 중, `axios.post` 메소드의 매개변수 자리에 주어진 3가지 항목을 이렇게 이해하였습니다.

- 첫번째 : 요청이 도달할 서버의 엔드포인트
- 두번째 : 요청에 넣어줄 값 (req.body)
- 세번째 : CORS 에러 해결을 위한 코드(?)

&nbsp;저는 이 `{ withCredentials: true }` 부분을 포함한 코드를 작성하고, 서버 코드에서 `app.use(cors())` 라고만 작성해 주면, '모든 origin의 요청을 다 허가한다' 라고 이해하였습니다.

&nbsp;그러나 이렇게 해 주면 CORS 에러가 출력되기에, 서버의 위 부분을 아래와 같이 수정하여 문제를 해결하였습니다.

```js
app.use(
  cors({
    origin: ["http://localhost:3000"],
    methods: ["GET", "POST", "PUT", "DELETE"],
    credentials: true,
  })
);
```

&nbsp;서버에서도 `cors()` 미들웨어 활용시에 `credentials: true,` 옵션을 줘야 CORS 에러가 해결되는 점을 확인하였습니다.

&nbsp;이 부분에 관하여, 다음 글들을 참고하여 더 공부하도록 하겠습니다.

- [Access-Control-Allow-Credentials](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Access-Control-Allow-Credentials)
- [XMLHttpRequest.withCredentials](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/withCredentials)
- [[WEB] withCredentials 옵션](https://kosaf04pyh.tistory.com/152)

<br>
<br>

---

&nbsp;프로젝트를 시작하면서, 앞의 스프린트에서 배웠지만 잊어버리고 지나간 것들이라던가, 별 생각없이 써 왔지만 에러로 만나서 비로소 공부할 기회를 얻은 것들 등을 만나고 있습니다.

&nbsp;앞으로도 이런 식으로, 조금씩이라도 기록에 남겨두도록 하겠습니다.
