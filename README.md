# 비주얼 스튜디오 코드 한스펠

[비주얼 스튜디오 코드 한스펠](https://github.com/9beach/vscode-hanspell)(vscode-hanspell)은, (주)다음과 부산대학교 인공지능연구실/(주)나라인포테크의 웹 서비스를 이용해서 한글 맞춤법 검사 기능을 제공하는 [비주얼 스튜디오 코드](https://code.visualstudio.com)용 [익스텐션](https://code.visualstudio.com/docs/editor/extension-marketplace)입니다.

터미널과 커맨드 라인 팬이라면 [hanspell](https://github.com/9beach/hanspell)을 추천합니다.

## 설치

[비주얼 스튜디오 코드 마켓 플레이스](https://marketplace.visualstudio.com/items?itemName=9beach.vscode-hanspell) 또는 비주얼 스튜디오 코드 익스텐션 탭에서 '한스펠'로 검색해서 설치합니다.

## 주요 기능 및 사용법

### 맞춤법 검사

아래의 그림과 같이 명령 팔레트(`⇧⌘P` 또는 `F1`)에서 맞춤법 검사를 실행할 수 있습니다.

명령 팔레트의 오른쪽, 톱니바퀴 아이콘을 클릭해서 핫키를 지정할 수 있습니다. 맞춤법 검사는 자동으로 실행되지 않으니 핫키를 권합니다.

마우스로 드래그해서 문서의 특정 영역을 선택한 상태라면 해당 영역만 검사합니다. 유용하지만 주의가 필요합니다.

![commands](https://github.com/9beach/vscode-hanspell/raw/HEAD/images/hanspell-commands.png)

### 맞춤법 교정

맞춤법 검사를 마치면 오류가 의심되는 문자열에 붉은 밑줄이 생깁니다. 해당 문자열을 클릭하면 왼쪽에 녹색 전구가 생기고, 다시 이것을 클릭하면 아래와 같이 추천 단어와 `맞춤법 오류 모두 교정` 메뉴가 뜹니다. 원하는 항목을 선택해서 맞춤법을 교정하세요. 물론 직접 입력해서 교정할 수도 있습니다.

![command actions](https://github.com/9beach/vscode-hanspell/raw/HEAD/images/hanspell-command-actions.png)

### 맞춤법 오류 정보

마우스를 붉은 밑줄 위로 옮기면 맞춤법 오류 정보가 뜹니다. 아래와 같이 결과 창(`⇧⌘M`)에서 한눈에 볼 수도 있습니다. (주)다음의 서비스에 비해 맞춤법 오류 정보가 충실하다는 점은 부산대 서비스의 장점입니다만 접속 장애가 잦다는 단점도 있습니다.

![message](https://github.com/9beach/vscode-hanspell/raw/HEAD/images/hanspell-problems.png)

### 맞춤법 검사 제외 단어 지정

톨스토이를 톨스또이로 쓰되 맞춤법 검사는 피하고 싶다면 홈 디렉터리에 `.hanspell-ignore` 파일을 만들고 '톨스또이*'를 등록하세요.

```txt
톨스또이*
이딸리아
```

위와 같이 등록하면 맞춤법 오류 중 '톨스또이', '톨스토이가' 등 '톨스또이'로 시작하는 것은 제외하고 표시합니다. 반면 '이딸리아'는 제외하지만 '이딸리아에서'는 오류로 표시합니다.

 `.hanspell-ignore`는 [글로브 패턴](https://ko.wikipedia.org/wiki/글로브_(프로그래밍))을 지원합니다. 마크다운 문법과 URL, 영어 등을 맞춤법 검사에서 제외하고 싶다면 아래의 예를 참고하세요.

```txt
[[!.a-zA-Z0-9:<>]*[[!.a-zA-Z0-9:<>]*
*[[!.a-zA-Z0-9:<>]*[[!.a-zA-Z0-9:<>]*
*[[!.a-zA-Z0-9:<>]*[[!.a-zA-Z0-9:<>]*/**
```

## 알려진 문제점

버그와 개선점은 [이슈 트래커](https://github.com/9beach/vscode-hanspell/issues)에 올려주세요.

### 중복된 맞춤법 오류에 의한 `맞춤법 오류 모두 교정` 커맨드 실패

부산대 맞춤법 서비스는 오류가 중복될 때가 있습니다. 예컨대 '채마밭'을 검사하면, '채마'는 '채소'로, '채마밭'은 '채소밭'으로 교정하도록 권합니다. 즉 '채마'라는 단어가 두 가지 교정 제안에 걸쳐 있습니다. 이런 상황이 더 복잡하게 얽혀서 `맞춤법 오류 모두 교정` 커맨드가 실패할 수 있습니다. 한 단어씩 교정하면 제대로 작동합니다.
