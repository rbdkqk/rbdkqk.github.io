---
title: '개발환경 새롭게 꾸미기'
excerpt: 'M1 Silicon Macbook Air'

categories:
  - etc
tags:
  - m1 silicon
  - dev env setting
last_modified_at: 2021-01-19
---

---

&nbsp;'어차피 취업하면 써야 할 것 같으니 빨리 익숙해지면 좋겠지' 라는 생각으로, 작년 말일날 맥북을 구입했습니다.

&nbsp;최근 새로 발표되어 판매중인 M1 Silicon이 포함된 맥북 에어인데, 이는 ARM 아키텍쳐를 반영했기에 인텔의 칩을 사용하던 기존 맥북과는 명령어 체계가 달라서, 사용하는 프로그램의 호환성을 신경써 줘야 한다고 들었습니다.

&nbsp;그래서 가급적 이를 신경써서 개발 환경을 구성하려고 노력하는 중인데, 잘 되고 있는 것인지 모르겠습니다.

&nbsp;M1 Silicon 맥북에서 개발환경을 구성하면서 만났던 문제들과 선택했던 해결방법들을 남겨두고, 나중에 제가 까먹었을 때 또 와서 보겠습니다. 틀린 점이 있다면 rbdkqk@gmail.com 으로 간단히 남겨주시면 정말 감사하겠습니다.

<!--

---

# 1. NVM, Node.js,

&nbsp;전에 쓰던 저장소에서 뭔가 가져오려면 `git`을 사용해야 하고, 가져와서 `node_modules`를 설치하려면 `node.js`와 `NPM`이 필요하고, node.js와 NPM을 위해서는 NVM이 필요했습니다.

-->

---

# VSCode Insiders // Finder App

## 1. 터미널에서 `code .` 명령어로 VSCode 열기

&nbsp;VScode는 아직 ARM 아키텍쳐를 위한 정식 버전이 배포되지 않았다고 합니다. 다만 Insiders 버전은 M1 맥에 대응한다고 해서, 정식버전이 아닌 Insiders 버전을 선택했습니다.

&nbsp;잘 모르는 단축키만 새롭게 찾아가면서 하나하나 해 가고 있었는데, 전에 사용하던 두 가지 기능이 작동하지 않았습니다.

- 터미널에서 `code .`을 입력해서, 현재 위치에서 VSCode 열기
- (탐색기 또는 Finder에서) 폴더를 우클릭하고 드롭다운 메뉴를 선택해서, 해당 폴더를 VSCode로 열기

&nbsp;둘 다 VSCode의 기능이라기보다는 VSCode를 좀더 쉽게 열기 위한 방법인데, 전엔 별 생각 없이 쉽게 했던 것들인데도 이번에는 나름 애먹었습니다.

&nbsp;먼저 첫번째 방법에 관하여 구글 등에 검색하면, VSCode에서 명령 팔레트를 열고(`⌘ + ⇧ + P` // `command + shift + P`) 아래 명령어를 입력하라고 합니다.

- `Shell Command : install 'code' command in PATH`

&nbsp;사실 Shell까지만 입력해도 자동완성으로 잡아주기 때문에 편하게 설정할 수 있어서, 저는 처음에는 이 부분을 자세히 보지 않고 넘어갔습니다.

&nbsp;이렇게만 해도 된다는 글도 있었는데, 이는 터미널을 끄거나 VSCode를 끄면 그 뒤에 이 명령어를 다시 입력해도 동작하지 않는 문제가 있습니다.

&nbsp;그래서 [이 글](https://helloinyong.tistory.com/223)을 참고해서, `~/.zshrc` 파일에 아래 코드를 추가했습니다. (글 작성자 분 감사드립니다.) (위 파일은 컴퓨터 root 폴더에 숨김파일로 들어가 있었습니다.)

- `code () { VSCODE_CWD="$PWD" open -n -b "com.microsoft.VSCode" --args $* ;}`

&nbsp;그 뒤 터미널을 껐다가 다시 열고 원하는 폴더로 가서 `code .` 명령어를 실행하면, 정상 동작할 줄 알았지만 아래와 같은 메세지가 나오고 VSCode가 동작하지 않습니다.

- `LSCopyApplicationURLsForBundleIdentifier() failed while trying to determine the application with bundle identifier com.microsoft.VSCode.`

&nbsp;그래서 원인을 찾다가, VSCode에서 `Shell Command`를 입력하는 것부터 다시 해 보던 중, 아래와 같은 내용을 발견했습니다.

&nbsp;VSCode에서 입력했던 명령어는 사실 자세히 보면 위 문구가 아니라 아래와 같이 표기됩니다.

- `Shell Command : install 'code-insiders' command in PATH`

&nbsp;차이는 `code`와 `code-insiders`였습니다.

&nbsp;혹시나 싶어서 터미널을 켜고 명령어 역시 `code-insiders .` 이렇게 입력하니, 정상 작동하는 것을 볼 수 있었습니다.

---

## 2. Finder App에서 폴더 우클릭 - 드롭다운 메뉴에서 VSCode 열기

&nbsp;위 방법도 종종 사용하지만, 저는 ubuntu를 사용하면서 어떤 폴더를 VSCode로 열어야 할 때, 폴더를 우클릭하고 드롭다운 메뉴를 통해 VSCode를 여는 방식을 많이 사용했었습니다.

&nbsp;맥북의 Finder에서도 비슷한 기능이 있을 것이라고 생각했었는데, 생각보다 찾기 어려웠습니다.

&nbsp;이번에도 다른 분께서 작성하신 [블로그 글](https://oddcode.tistory.com/126)을 참고했습니다. (작성자 분 정말 감사합니다.)

- 설치되어 있는 앱 중 `Automator`를 첮아서 열고,
- 상단 메뉴에서 `파일-신규` 선택 후 문서 유형 선택에서 `서비스`를 선택한 뒤,
- '현재 수신하는 작업흐름'에서 `파일 또는 폴더`, '선택 항목 위치'에서 `Finder.app` 선택 후,
- 좌측 메뉴에서 `보관함`, 그 우측 메뉴에서 `셸 스크립트 실행`을 찾아서 이를 우측에 드래그해서 놓고,
- 우측 '통과 입력' 란에서 `변수`를 선택한 뒤,
- `open -n -b "com.microsoft.VSCode" --args "$*"` 이 코드를 복사해 넣고,
- `Open in Visual Studio Code` 등의, 원하는 이름으로 저장힙니다.

&nbsp;이렇게 한 뒤, Finder에서 원하는 폴더를 우클릭(두 손가락 동시 누르기)한 후, `빠른 동작` 항목으로 가면, 위에서 적은 이름의 선택지를 볼 수 있습니다.

&nbsp;문제는, 이렇게 해 주고 해당 선택지를 누르면, 아래와 같은 메세지가 또 나온다는 것입니다.

- `‘셸 스크립트 실행’ 동작에 오류가 발생함: ‘LSCopyApplicationURLsForBundleIdentifier() failed while trying to determine the application with bundle identifier com.microsoft.VSCode.’`

&nbsp;저는 이번에도 비슷한 경우라고 생각하고, 위에서 작성한 `open -n -b "com.microsoft.VSCode" --args "$*"` 이 코드를 아래와 같이 수정했습니다.

- `open -n -b "com.microsoft.VSCodeInsiders" --args "$*"`

&nbsp;이번에도 `Insiders`라는 단어를 덧붙여서 시도했는데, 다행히도 정상 작동하는 것을 볼 수 있었습니다.

&nbsp;아울러, '폴더 우클릭 - 빠른 동작 메뉴 - VSCode 열기 메뉴 클릭'의 3단계를 더 줄이면 좋겠다는 생각에, 키보드 단축키를 이용할 수 있는 방법을 찾아보았습니다.

&nbsp;'시스템 환경설정 - 키보드 - 단축키' 탭으로 이동하고,

- 좌측의 '서비스' 선택 후, 우측 메뉴 중 '파일 및 폴더' 하위메뉴 중 앞에서 정한 명칭(제 경우는 `Open in Visual Studio Code`)을 찾아, 앞에 체크박스가 꺼져 있다면 체크해 주고,
- 해당 메뉴 우측의 '없음' 또는 '단축키 추가' 부분을 클릭하여, 원하는 키보드 버튼 조합으로 단축키를 만듭니다.

&nbsp;저는 VSCode니까 V를 넣고 싶었는데, `⌘ + ⌥ + ⇧ + V`를 입력하니 동작하지 않아서, `⌘ + ⌥ + ⇧ + P`를 설정해 두었습니다.

&nbsp;이제 Finder에서 원하는 폴더를 선택만 한 뒤, 우클릭 없이 위 단축키를 누르면 해당 폴더 위치에서 VSCode가 곧바로 실행됩니다.

---

&nbsp;VSCode의 Insiders 버전을 사용하게 되면서, 위 두 가지를 쓰기 위해 나름 시행착오를 겪었습니다.

&nbsp;사실 이에 앞서서 `NVM` 설치, `Node.js` 설치 등에서도 굉장히 헤맸는데, 어찌저찌 해결을 하고 나니 구체적인 해결 방법이 기억에서 날아가 버려 아쉽습니다.

&nbsp;이번 글도 잊어버리기 전에 적어둬야겠다는 생각으로 작성했는데, 사실 제가 한 것은 굉장히 간단한 수정이었지만 그래도 원하는 기능을 사용할 수 있게 되어 다행이라고 생각합니다.

&nbsp;앞으로도 M1 Silicon 맥북을 사용하면서 이런저런 무언가를 만나게 되면, 이 글에 이어서 수정해 나가면 좋겠습니다.
