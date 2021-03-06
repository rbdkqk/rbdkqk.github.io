---
title: "두번째 프로젝트 - TIL (Today I Learned)"
excerpt: "할일과 리뷰 위주의 캘린더 앱"

categories:
  - Second Project
tags:
  - Javascript
  - Second Project
  - Frontend
last_modified_at: 2020-11-12
---

# &nbsp;&nbsp; 두번째 프로젝트 - "TIL"

&nbsp;사실 이미 두번째 프로젝트가 시작되었는데, 도저히 글로 남길 시간을 내지 못해서 일주일정도 늦은 시점에서 첫 기록을 남깁니다.

&nbsp;코드스테이츠 공부도 이번 프로젝트로 마무리되는데, 교육과정중에 블로그를 잘 남기지 못했습니다. 그날그날 시도했던 사항들(todo)과 그 사항을 실제 시도해 나갔던 기록들(review)을 일목요연하게 정리할 필요를 느꼈습니다.

&nbsp;이 기록을 남기는 형태에 관하여, git의 commit 기록들처럼 순차로 나열해서 정리되면 공부해 나갔던 흐름을 잘 알 수 있고 블로그 작성에도 도움이 될 것이라고 의견이 모였습니다.

&nbsp;그래서 기존의 Todo앱, 캘린더 혹은 일정관리 앱의 기능에서 위와 같은 점이 부족하다고 생각하였기에, 이를 보완한 웹앱을 만드는 것을 프로젝트 목표로 삼게 되었습니다.

&nbsp;아이디어 내지는 취지에 맞게 앱의 이름(프로젝트 이름)을 "TIL (Today I Learned)"라고 짓게 되었습니다.

&nbsp;코드스테이츠 교육과정 전체는 물론이고 특히 앞선 프로젝트를 진행하면서 기록을 많이 남기지 못해 굉장히 아쉽습니다. 이번 프로젝트에서는 최대한 기록을 남겨가며 참여하려고 합니다.

&nbsp;이번 프로젝트의 팀 구성원은 저를 포함하여 총 3명이며, 서버 담당 1명과 클라이언트 담당 2명으로 구성되었습니다. 저는 이번 프로젝트에서도 클라이언트 구현에 참여하였기에, 앞으로의 내용 역시 클라이언트 구현에서 만난 일들 위주로 작성할 것으로 보입니다. 물론 서버에서 함께 고민한 점도 기록할 수 있다면 좋겠습니다.

---

<br>
<br>

## 1. SR (Software Requirements)

&nbsp;이번 프로젝트 역시 SR 과정을 진행하였습니다. 프로젝트의 목적과 구현하고자 하는 기능, 이를 위해 필요한 사항 전반에 관하여 이야기를 나누었습니다.

&nbsp;앞선 프로젝트와 구성원이 앞선 프로젝트와 동일하였기 때문에, 이전 프로젝트에서 아쉬웠던 점을 특히 고민하였습니다.

- 로그인 유지에 관하여 cookie를 사용하여 기능 동작이 원활하지 못함
- `Bootstrap`을 이용한 페이지 디자인 구현에 취약했음
- 기능 면에서 빠르게 의견을 받아 더 많은 기능을 구현하려 했으나 그러지 못함
- 소셜로그인 기능을 구현하지 못함

&nbsp;반대로, 규모가 작은 프로젝트였으므로 `Redux`를 활용할 필요가 크지는 않았으나, 공부하는 의미에서 이를 반영했던 점은 나름 도움이 되었다고 생각합니다. Functional Component로 구성하면서 상태관리 등을 위해 `React Hooks`를 사용해 본 것도 좋았습니다. 서버에서는 기존 스프린트에서 1개의 또는 2개 정도의 테이블만을 활용하였으나, 여러 테이블간에 상호 연결된 구조를 구현해 보는 등 새롭게 배운 점이 있었습니다.

&nbsp;이번 프로젝트에서는 아래와 같은 점을 논의하였습니다.

- 로그인 부분에서 `JWT`를 적용하기
- 소셜로그인 기능 반영하기
- CSS에 관하여 다시한번 `Bootstrap`을 활용하기
- 기본적인 기능 구현을 최대한 빠르게 마무리한 뒤, 보다 도전적인 과제를 찾아 추가로 구현하기. (캘린더 공유 기능, 드래그 앤 드랍 기능 등등)

&nbsp;무엇보다도 이번 프로젝트에서는 현업에서 상당히 쓰인다는 `TypeScript`를 서버와 클라이언트 양쪽에서 반영하기로 하였습니다.

---

<br>
<br>

## 2. 첫 일주일간 만났던 문제

&nbsp;첫번째 일주일간에는 프로젝트 아이디어를 선정하고 이를 위한 기본 사항들에 관하여 대화를 나누었습니다.

&nbsp;위에서 나열한 기존 프로젝트의 회고와 새로운 프로젝트에 반영할 내용들 위주의 회의가 진행되었습니다.

&nbsp;그 뒤, 기본적인 회원가입/로그인/로그아웃/소셜로그인/마이페이지 정도를 먼저 구현하는 것으로 의견을 모으고, 역할에 맞게 코드 작성을 시작하였습니다.

&nbsp;'위에 나열한 5가지 페이지 또는 기능을 일주일이면 구현할 수 있지 않을까...?' 라고 생각했으나, 실제로는 그렇지 못했습니다. 생각보다 기본 세팅에 상당한 시간이 소요되고 말았습니다.
<br>
<br>

### (1) TypeScript 설정과 Prettier 적용

&nbsp;기본적인 TypeScript 적용을 너무 쉽게 생각하여 이런저런 문제가 생겼습니다.

&nbsp;설치하고 설정만 잠깐 조정하면 문제가 없겠거니 라고 단순하게 생각했었는데, 코드 구성 통일을 위해 도입하기로 했던 `Prettier`를 함께 적용하는 것에서 문제가 길어졌습니다.

&nbsp;`TsLint`가 더이상 사용되지 않고 `ESLint`에 통합되었다거나, `ESLint`와 `Prettier`의 설정을 조정하는 것들을 원활하게 적용하지 못했습니다.

&nbsp;상당한 시간을 투자하여, 파일을 저장할 때 `Prettier`가 작동하여 코드가 정리되도록 만들 수 있게 되었습니다.

&nbsp;이전 프로젝트에서, 함께 코드를 작성하는 동료와 코드 작성 스타일(?)을 맞추지 않아서 내용변경이 전혀 없더라도 코드구성이 변경되어 버리고, 이 때문에 상호간에 코드 형태에 차이가 생기는 것이 저 혼자만 속으로 불편했던 점이었습니다. `Prettier`와 같은 도구를 함께 사용해서 규칙을 맞추면 좋겠다고 생각했었는데, 이번 프로젝트에서는 이 부분을 챙길 수 있었습니다.
<br>
<br>

### (2) 디자인 패턴 적용하기 - `Atomic Design`

&nbsp;이전 프로젝트에서는 `Redux` 상태관리를 위한 `modules 폴더`, 그렇게 변경된 상태를 반영하여 view(?) 부분에 내려보내주는 `container 폴더`, 이러한 상태를 매번 받아서 화면에 다르게 표시하는 `component 폴더` 3가지로 큰 틀을 잡고 코드를 작성했었습니다.

&nbsp;이런 구성이 프로젝트 코드의 디자인 패턴 면에서는 적절하지 않을 수 있다고 생각되었기에, 그리고 배우는 입장에서 디자인 패턴을 하나 선택하여 적용해 보는 것이 의미가 있겠다는 의견 덕분에, 이번 프로젝트에서는 `Atomic Design`을 적용해서 클라이언트를 구성해 보기로 하였습니다.

&nbsp;`Atomic Design`은 재사용 가능한 컴포넌트를 만들기 위한 목적을 충실히 따르는 디자인 패턴이라고 생각합니다. 프로젝트에 사용되는 각 구성부분을 원자 단위부터 아주 작게 쪼개고, 이를 조합해 나가는 방식으로 구성해 나가게 됩니다.

&nbsp;`Atom -> Molecule -> Organism -> Template -> Page` 순서로 컴포넌트들이 작성되어 나열되어, 이런 단위별로 재사용이 가능하고 유지보수에 유리하도록 하는 점이 큰 장점이라고 합니다.

&nbsp;이를 반영해 보기 위해, 쓰이는 하나하나의 요소들(텍스트, 입력창, 버튼 등)을 작은 조각의 컴포넌트로 작성하고 이를 조합해 나가는 방식으로 화면을 구성해 보았습니다.

&nbsp;그러나, 결론부터 이야기해서 당장은 이 `Atomic Design` 적용을 미루기로 하였습니다.

&nbsp;회원가입 페이지에서 먼저 적용해 보았는데, 페이지가 어떻게 생겼는지를 실제 코드로 일단 구현하는 `mock-up`을 거치는 과정에서부터, CSS 능력 부족으로 시간이 너무 많이 소요되었습니다.

&nbsp;또한 기본 `Javascript`가 아닌 `TypeScript`를 활용하려다 보니, 이를 에러없이 적용하기 위해 소요되는 시간이 굉장히 길어지게 되었습니다.

&nbsp;이러다가는 기본적인 기능구현에도 너무 긴 시간이 소요될 수 있어서, 일단 기능구현에 먼저 착수하고 기능이 잘 구현되면 이를 `Atomic Design`의 디자인 패턴으로 수정해 보기로 결정을 변경하게 되었습니다.

---

<br>
<br>

## 3. 첫 주를 마무리하며,

&nbsp;프로젝트 시작하는 첫 날에 이 블로그 글을 남기려는 것이 원래 생각이었으나, 실제의 코드를 작성하기도 전에 위와 같은 점을 해결하느라 너무 많은 시간이 소요되고 말았습니다.

&nbsp;첫 주부터 큰 성과가 나지 않았다는 생각에 굉장히 조급한 마음이 생기지만, 이런 새로운 문제를 경험해 보고 이를 해결해 가는 과정 역시 저와 동료 분들에게 도움이 되었을 것이라고 생각합니다.

&nbsp;앞으로는 실제의 기능을 구현해 가면서 새롭게 배우는 내용들이나 만나는 문제들에 관해 적도록 하겠습니다.

&nbsp;이번 프로젝트가 잘 마무리된다면, 앞으로도 코딩을 공부하면서 블로그를 꾸준히 작성하는데에 있어서, 제가 참여한 `TIL` 앱으로 제가 도움을 받을 수 있을 것 같아 기대가 됩니다.
