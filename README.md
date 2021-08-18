# 비주얼 스튜디오 코드 한스펠

_이 문서의 최신 버전은 [깃허브](https://github.com/9beach/vscode-hanspell/blob/main/README.md)에서 찾을 수 있습니다._

[비주얼 스튜디오 코드 한스펠](https://github.com/9beach/vscode-hanspell)(vscode-hanspell)은, (주)다음과 부산대학교 인공지능연구실/(주)나라인포테크의 웹 서비스로 한글 맞춤법을 검사하는 [비주얼 스튜디오 코드](https://code.visualstudio.com)용 [익스텐션](https://code.visualstudio.com/docs/editor/extension-marketplace)입니다.

터미널과 커맨드 라인 팬이라면 [hanspell](https://github.com/9beach/hanspell)을 추천합니다.

## 설치

[비주얼 스튜디오 코드 마켓 플레이스](https://marketplace.visualstudio.com/items?itemName=9beach.vscode-hanspell) 또는 비주얼 스튜디오 코드 익스텐션 탭에서 “한스펠”로 검색해서 설치합니다.

## 주요 기능 및 사용법

### 맞춤법 검사

`Ctrl+Shift+P`(macOS `⇧⌘P`) 또는 `F1` 키로 명령 팔레트에서 맞춤법 검사를 실행합니다. `맞춤법 검사 (다음)`, `맞춤법 검사 (부산대)`, `맞춤법 검사 (다음, 부산대)`, 모두 세 개의 커맨드를 제공하는데, `맞춤법 검사 (다음, 부산대)`는 두 서비스를 한 번에 실행한 뒤 결과를 모아서 보여줍니다.

![commands](https://github.com/9beach/vscode-hanspell/raw/HEAD/images/hanspell-commands.png)

명령 팔레트의 오른쪽, 톱니바퀴 아이콘을 클릭해서 핫키를 지정합니다. 맞춤법 검사는 자동으로 실행되지 않아서 핫키를 추천합니다.

마우스로 드래그해서 문서의 특정 영역을 선택한 상태라면 해당 영역만 검사합니다. 유용하지만 주의가 필요합니다.

### 맞춤법 교정

맞춤법 검사를 마치면 오류가 의심되는 문자열에 물결 모양의 밑줄이 표시됩니다. `F8` 키를 누르거나 해당 문자열을 클릭하면 왼쪽에 녹색 전구가 뜹니다. 이것을 클릭하거나 `Ctrl+.`(macOS `⌘.`) 키를 누르면 추천어 등 교정 액션 메뉴가 뜹니다.

![command actions](https://github.com/9beach/vscode-hanspell/raw/HEAD/images/hanspell-command-actions.png)

`Shift+Alt+.`(macOS `⌥⌘.`) 키를 누르면 메뉴를 생략하고 바로 교정합니다. 다시 `F8` 키를 누르면 그다음 오류로 이동합니다.

`맞춤법 검사 (다음, 부산대)` 커맨드는 두 서비스가 공통으로 발견한 오류와 한 서비스만 발견한 오류를, 각각 오렌지색(Warning)과 파란색(Information)으로 구분합니다. 다른 두 커맨드는 모두 오렌지색으로 표시합니다.

### 맞춤법 오류 정보

마우스를 밑줄 위로 옮기면 맞춤법 오류 정보가 뜹니다. `Ctrl+Shift+M`(macOS `⇧⌘M`) 키를 눌러 결과 창에서 한눈에 볼 수도 있습니다. (주)다음 서비스보다 맞춤법 오류 정보가 충실하다는 점은 부산대 서비스의 장점이지만 접속 장애가 잦다는 단점도 있습니다.

![message](https://github.com/9beach/vscode-hanspell/raw/HEAD/images/hanspell-problems.png)

### 히스토리 파일

`~/.hanspell-history` 파일에는 맞춤법 교정 내용이 기록됩니다. 교정 액션 메뉴나 `Shift+Alt+.` 키를 이용하지 않고 직접 수정했다면 기록되지 않습니다.

파일 크기가 10MB를 넘으면 `.hanspell-history.N`(`N`은 1, 2, 3...)으로 백업한 뒤 새로 만듭니다.

아래는 사용자가 자주 틀리는 맞춤법을 빈도순으로 보여주는 셸 스크립트입니다. 리눅스나 macOS 환경에서만 작동합니다.

```console
$ sort < ~/.hanspell-history | uniq -c | sort -nr | head -n 5
  17 모래속에 -> 모래 속에
  13 그 뿐만 -> 그뿐만
  13 했는 지 -> 했는지
  13 한바퀴 -> 한 바퀴
   7 내노라하는 -> 내로라하는
```

### 맞춤법 검사 제외 문자열 지정

`톨스토이`를 `톨스또이`로 쓰되 맞춤법 검사는 피하고 싶다면 홈 디렉터리에 `.hanspell-ignore` 파일을 만들고 `톨스또이*`를 추가하세요.

```txt
톨스또이*
이딸리아
```

이제 `톨스또이`, `톨스토이가` 등 `톨스또이`로 시작하는 문자열은 맞춤법 오류에서 제외합니다. 반면 `이딸리아`는 제외하지만 `이딸리아에서`는 오류로 간주합니다.

`.hanspell-ignore`는 [globstar](https://www.linuxjournal.com/content/globstar-new-bash-globbing-option)를 포함한 [글로브 패턴](https://man7.org/linux/man-pages/man7/glob.7.html)을 지원합니다. 맞춤법 오류에서 URL을 제외하고 싶다면 다음을 추가하세요.

```txt
*http*/**
```

### 사용자 정의 맞춤법

`~/.hanspell-typos` 파일에 아래와 같이 사용자가 직접 맞춤법을 정의할 수 있습니다.

```txt
제임슨 -> 제머슨
엘지전자 -> LG전자
돈키호테 -> 돈 끼호떼
감사합니다 -> 고맙습니다
```

문서 작성 과정에서 자동으로 분석해준다는 점은 이 기능의 가장 큰 특징입니다. 새로 검사하기 전에는 최근 결과로 계속 분석하기 때문에 같은 실수를 반복하면 새로 검사하지 않아도 자동으로 밑줄이 표시됩니다. 이처럼 사용자 정의 맞춤법도 최근 검사에서 발견된 오류처럼 기능합니다.

아래는 자주 틀리는 맞춤법 20개로 `~/.hanspell-typos` 파일을 만드는 셸 스크립트입니다.

```bash
sort < ~/.hanspell-history | uniq -c | sort -nr | head -n 20 | sed -e 's:^  *[0-9][0-9]* \(.*\):\1:' > ~/.hanspell-typos
```

사용자 정의 맞춤법은 단어 단위로 적용됩니다. 즉 `돈키호테 -> 돈 끼호떼`를 등록하면 “돈키호테!”와 “돈키호테”에는 적용되지만 “돈키호테가”에는 적용되지 않습니다.

### 사용자 정의 표현식

[정규 표현식](https://ko.wikipedia.org/wiki/%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D)에 익숙하지 않은 사용자는 이 섹션을 건너뛰세요.

두음법칙에 의해 “님에게”가 아니라 “임에게”가 올바릅니다. 이것 때문에 “선생님에게”도 “선생임에게”로 고치는 우를 피하려면 단어 단위로 검색해야 합니다. (물론 한국어는 문맥 의존성이 커서 이것으로도 부족합니다.) 그래서 내부적으로는 “님에게”로 검색하지 않고 [“Lookahead and Lookbehind Zero-Length Assertions”](https://www.regular-expressions.info/lookaround.html)를 덧붙여서 `/(^|(?<=[^ㄱ-ㅎㅏ-ㅣ가-힣a-zA-Z]))님에게((?=[^ㄱ-ㅎㅏ-ㅣ가-힣a-zA-Z])|$)/g`로 검색합니다. 이런 이유로 원하는 단어가 포함된 다양한 표현을 **사용자 정의 맞춤법**으로 분석하기는 어렵습니다.

이 문제는 `~/.hanspell-bad-expressions.json`에 사용자가 직접 정규 표현식을 작성해서 어느 정도 해결할 수 있습니다. 다음 예를 봅시다.

```json
{
  "bad-expressions": [
    {
      "expression": "돈키호테",
      "info": "우리 프로젝트의 공식 표기는 “돈 끼호떼”입니다.",
      "suggestions": ["돈 끼호떼"],
      "severity": "Error"
    },
    {
      "expression": "([가-힣]+)의 +([가-힣]+)의((?=[^ㄱ-ㅎㅏ-ㅣ가-힣a-zA-Z])|$)",
      "info": "‘-의’를 겹쳐 쓰면 어색합니다.",
      "suggestions": ["$1 $2의"],
      "severity": "Warning"
    },
    {
      "expression": "[가-힣]+[을를] +[^.,\"“”]+[가-힣][을를]((?=[^ㄱ-ㅎㅏ-ㅣ가-힣a-zA-Z])|$)",
      "info": "한 문장에 ‘-을(를)’이 두 번 이상 나옵니다."
    },
    {
      "expression": "([가-힣]*게 (된|됩|되)|[가-힣]*고 있|보여 [주준줍]|처해 있|다름 아[니닙닌]|[가-힣]*져 있)[가-힣]+",
      "info": "군더더기 있는 표현입니다.",
      "severity": "Information"
    }
  ]
}
```

첫 번째 표현식은 “돈키호테” 좌우에 “Lookahead and Lookbehind”가 없어서 “돈키호테는”, “돈키호테가” 등에 모두 적용됩니다.

두 번째 표현식은 “우리의 사랑의”처럼 ‘-의’를 겹쳐 쓴 표현을 “우리 사랑의”로 고치도록 설정합니다.

세 번째 표현식은 “그 사람을 결국에는 신뢰를 했다”처럼 한 문장에서 ‘-을(를)’이 두 번 이상 나오면 밑줄을 긋도록 설정합니다.

네 번째 표현식은 “하게 되었습니다”, “알려져 있다”, “보여 주고” 등과 같이 군더더기 있는 표현에 밑줄을 긋도록 설정합니다.

[형태소](https://ko.wikipedia.org/wiki/%ED%98%95%ED%83%9C%EC%86%8C)를 분석하지 않고 정규 표현식에 의존하는 것은 한계가 분명합니다. “세계의 불가사의”는 문제없는 표현이지만 위의 설정으로는 ‘-의’를 겹쳐 썼다고 분석됩니다. 주의해서 사용하시기 바랍니다.

`.hanspell-bad-expressions.json`에 `info`, `suggestions`, `severity`는 정의하지 않아도 되지만 `expression`은 정의해야 합니다. `severity`는 심각도에 따라 `Error`, `Warning`, `Information` 중 하나를 지정하세요.

## 알려진 문제점

버그와 개선점은 [이슈 트래커](https://github.com/9beach/vscode-hanspell/issues)에 올려주세요.

### 중첩된 맞춤법 오류에 의한 `맞춤법 오류 모두 교정` 액션 실패

`맞춤법 검사 (다음, 부산대)` 커맨드로 분석한 오류는 가끔 중첩될 때가 있습니다. 예를 들어 `abc def ghi...`와 같은 문장에서, `abc def`와 `def`가 모두 맞춤법 오류라면 `def`는 두 오류에 걸쳐 있습니다. 이런 식으로 복잡하게 얽히면 `맞춤법 오류 모두 교정` 액션이 실패할 수 있습니다. `다음, 부산대 공통 오류만 모두 교정` 액션은 이때에도 대부분 제대로 작동합니다.

### 긴 문장 교정 시 부산대 맞춤법 서비스의 잦은 접속 오류

서버 제약으로 긴 문장은 짧은 문장 여러 개로 나누어 요청합니다. 부산대 서비스는 이런 경우 자주 실패합니다.
