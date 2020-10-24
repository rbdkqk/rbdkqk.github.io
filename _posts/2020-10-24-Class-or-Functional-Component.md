---
title: "첫 프로젝트 - Component 선택"
excerpt: "Class Component vs Functional Component"

categories:
  - First Project
tags:
  - Javascript
  - First Project
  - Frontend
last_modified_at: 2020-10-24
---

&nbsp;회원가입과 로그인 기능을 작성하던 중, 문제가 발생하였기에 기록해 두려고 합니다.

&nbsp;두 기능을 위한 두 코드 모두에서 같은 문제가 발생하였으며, 아래에서는 로그인 코드만 기록해 두겠습니다.

---

<br>
<br>

## 1. 로그인 기능의 기존 코드

&nbsp;기존 작성한 로그인 코드는 Functional Component로 구성하였으며, 아래와 같은 코드입니다.

```js
import React from "react";
import { connect } from "react-redux";
import { loginRequest } from "../actions/authentication";
import { Login } from "../components";

function LoginContainer(props) {
  // console.log("props.status : ", props.status); // 여기서는 Waiting Success로 잘 나온다
  function handleLogin(id, pw) {
    // 아래의 connect 덕분에 loginRequest 메소드를 props 로 넘겨받을 수 있음 ("from "../actions/authentication";")
    return props.loginRequest(id, pw).then(() => {
      // console.log("props.status : ", props.status); // INIT 이 나와버린다. props.loginRequest(id, pw)의 결과를 기다리지 않고 다음으로 넘어가고 있음
      if (props.status === "SUCCESS") {
        // create session data
        let loginData = {
          isLoggedIn: true,
          username: id,
        };

        // (쿠키에 저장할 때 객체를 만든 뒤, 해당 객체를 문자화(JSON.stringify 메소드) 시키고 base64 로 인코드한 뒤, 앞에 'key=' 를 붙여 저장합니다)
        // * 쿠키에 저장된 값을 이용하여 로그인 했는지 여부를 판단합니다.
        // * btoa 는 base64 로 인코드 하는 메소드입니다. 이에 대해 익숙치 않으신 분들은 아래의 링크를 참조해 주세요.
        // * base64 인코드, 디코드 메소드 - btoa(), atob() : https://pro-self-studier.tistory.com/106?category=659555
        document.cookie = "key=" + btoa(JSON.stringify(loginData));

        props.history.push("/"); // 리디렉트
        return true;
      } else {
        alert(`로그인에 문제가 있습니다. 다시 시도해 주세요.`);
        return false;
      }
    });
  }

  return (
    <div>
      <Login handleLogin={handleLogin} />
    </div>
  );
}
```

```js
const mapStateToProps = (state) => {
  return {
    status: state.authentication.login.status,
  };
};

const mapDispatchToProps = (dispatch) => {
  return {
    loginRequest: (id, pw) => {
      return dispatch(loginRequest(id, pw));
    },
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(LoginContainer);
```

&nbsp;위 `LoginContainer` 컴포넌트는 Redux와 연결되어 store의 state를 받아오기 위한 컴포넌트입니다.

&nbsp;이렇게 받아온 '상태'를, 리턴 부분의 `Login` 컴포넌트로 넘겨주기 위한 역할이며, 이 `Login` 컴포넌트에서 실제의 email 및 password 입력값을 받아 기능을 실행합니다.

<br>
<br>

## 2. 문제 발생

&nbsp;위 코드는 물론 Reducer 등을 거치게 되며, 이런 처리에서 `status`로 받아오는 `state.authentication.login.status`의 변화는 다음과 같습니다.

- 최초 : "INIT"
- 시작(로그인 요청 시작) : "WAITING"
- 성공(로그인 성공) : "SUCCESS"
- 실패(로그인 실패) : "FAILURE"

&nbsp;따라서, 로그인 요청이 시작되어 성공했다면, 위 값은 "INIT" => "WAITING" => "SUCCESS" 순서로 변경될 것입니다.

&nbsp;저는 위 작성된 클라이언트 코드에서 이런 순서의 흐름이 잘 적용될 것이라고 생각했습니다.

&nbsp;그런데, 기능을 작동한 뒤 크롬 console에 표시되는 위 값은 "WAITING"과 "SUCCESS"로 잘 표시되었지만, 정작 기능은 실행되지 않고, 위 코드 중 ` else { alert(`로그인에 문제가 있습니다. 다시 시도해 주세요.`); return false; }` 부분으로 넘어가고 있었습니다.

&nbsp;그래서 `props.status` 값이 제대로 변경되고 있는지를 추적하기 위해, 위와 같이 `handleLogin` 함수 안과 밖 모두에서 `props.status` 값을 console에서 확인해 보았는데, 위 함수 밖에서는 정상적으로 변경되는 것처럼 나왔지만, 함수 안에서는 "INIT"인 상태 그대로인 것을 확인하였습니다.

<br>
<br>

## 3. 판단 및 해결(?)

&nbsp;저는 위 코드가 아래와 같이 작동할 것이라고 이해하고 있었습니다.

> `props.loginRequest(id, pw).then(() => { ... }` 중에서,
> `props.loginRequest(id, pw)` 부분이 먼저 실행되어,
> `props.status`값이 "INIT" => "WAITING" => "SUCCESS" 순서로 잘 변경된 뒤,
> 그 이후에야 `.then()` 부분이 실행될 것이고, 그 때에 `props.status` 값은 상태(store) 변경을 모두 마친 "SUCCESS" 상태일 것이니,
> `if (props.status === "SUCCESS") { ... }` 이하로 잘 들어갈 것이다.

&nbsp;그러나 제 의도와는 달리, 실제로는 `props.loginRequest(id, pw)` 부분의 실행결과를 기다리지 않고 곧바로 `.then()` 부분이 실행되어, 아직 `props.status` 값이 변경되지 않은 최초의 "INIT"인 상태이므로, else 이하로 코드가 들어간 것으로 보입니다.

&nbsp;이 문제를 해결하기 위해 나름 이것저것 팀원 분들과 함께 수정해 보았으나, 결국 모두 실패하였습니다.

&nbsp;팀원 분께서는 위 발행한 문제가 "context의 문제가 아닌가" 라고 짚어 주셨고, `props`를 class의 `this`로 받아오면 해결될 것 같다고 해 주셨습니다.

&nbsp;아래와 같이 Class Component 형태로 구성해서 정상 작동하는 것을 확인했습니다.

```js
import React, { Component } from "react";
import { connect } from "react-redux";
import { loginRequest } from "../actions/authentication";
import { Login } from "../components";

class LoginContainer extends Component {
  handleLogin = (id, pw) => {
    // 아래의 connect 덕분에 loginRequest 메소드를 props 로 넘겨받을 수 있음 ("from "../actions/authentication";")
    return this.props.loginRequest(id, pw).then(() => {
      // console.log("props.status : ", props.status); // INIT 이 나와버린다. props.loginRequest(id, pw)의 결과를 기다리지 않고 다음으로 넘어가고 있음
      if (this.props.status === "SUCCESS") {
        // create session data
        let loginData = {
          isLoggedIn: true,
          username: id,
        };

        // (쿠키에 저장할 때 객체를 만든 뒤, 해당 객체를 문자화(JSON.stringify 메소드) 시키고 base64 로 인코드한 뒤, 앞에 'key=' 를 붙여 저장합니다)
        // * 쿠키에 저장된 값을 이용하여 로그인 했는지 여부를 판단합니다.
        // * btoa 는 base64 로 인코드 하는 메소드입니다. 이에 대해 익숙치 않으신 분들은 아래의 링크를 참조해 주세요.
        // * base64 인코드, 디코드 메소드 - btoa(), atob() : https://pro-self-studier.tistory.com/106?category=659555
        document.cookie = "key=" + btoa(JSON.stringify(loginData));

        this.props.history.push("/"); // 리디렉트
        return true;
      } else {
        alert(`로그인에 문제가 있습니다. 다시 시도해 주세요.`);
        return false;
      }
    });
  };

  render() {
    return (
      <div>
        <Login handleLogin={this.handleLogin} />
      </div>
    );
  }
}
```

```js
const mapStateToProps = (state) => {
  return {
    status: state.authentication.login.status,
  };
};

const mapDispatchToProps = (dispatch) => {
  return {
    loginRequest: (id, pw) => {
      return dispatch(loginRequest(id, pw));
    },
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(LoginContainer);
```

<br>
<br>

## 4. 아직 이해되지 않은 상태인데...

&nbsp;Class Component와 Functional Component가 어떤 차이를 가지기에 이런 문제가 생기는지, 제가 참고하여 작성했던 Functional Component의 코드에서는 어떤 부족한 점이 있었고, 왜 Class Component로 바꿔 주었을 때에는 문제가 해결된 것인지 궁금합니다.

&nbsp;기능 구현을 빠르게 진행해야 프로젝트 진도를 맞출 수 있기에, 이번에 겪은 이 문제를 일단 블로그의 글로만 적어 두고, 전체 코드를 다른 방식으로 다시 작성해서 계속 진행하겠습니다.
