# 설치와 설정

Jujutsu를 설치하는 방법은 다양하며, 어떤 방법이 최선인지는 시스템에 따라 다릅니다.
설치 방식에 전혀 신경 쓰고 싶지 않다면 아래 명령을 그대로 복사해 실행하세요.

```sh
curl https://mise.run | sh
~/.local/bin/mise install-into jujutsu@latest /tmp/jj-install
mv /tmp/jj-install/jj ~/.local/bin
rm -rf /tmp/jj-install
exec $SHELL --login
```

이제 `jj --version`으로 설치를 확인하세요.
`jj 0.35.0-blabla` 같은 현재 설치된 버전을 출력해야 합니다.
대신 `bash: jj: command not found...` 같은 오류가 나온다면 아래 상자를 펼쳐 보세요.

````admonish fail title="jj: command not found..." collapsible=true
여러분의 시스템은 설치 디렉터리 `~/.local/bin`을 `PATH` 환경 변수에 추가하지 않는 것 같습니다.
이를 해결하려면 어떤 셸을 쓰는지 먼저 알아야 합니다.

```sh
echo $SHELL
```

출력은 "bash" 또는 "zsh"로 끝날 겁니다.
그게 여러분의 셸입니다.
다음으로 셸 시작 스크립트에 `~/.local/bin`을 `PATH`에 추가하는 명령을 넣습니다.

```sh
# bash:
echo 'export PATH=$HOME/.local/bin:$PATH' >> ~/.bashrc
```

```sh
# zsh:
echo 'export PATH=$HOME/.local/bin:$PATH' >> ~/.zshrc
```

마지막으로 터미널을 닫았다가 다시 열어 변경 사항을 적용하세요.
````

```admonish note title="설치 명령 설명" collapsible=true
소프트웨어 설치는 생각보다 어렵습니다.
CPU 아키텍처, 운영체제 등 여러 요소에 따라 달라지죠.
그래서 어떤 시스템에서든 한 줄로 Jujutsu를 설치할 수 있는 간단한 명령은 존재하지 않습니다.
대신, 먼저 소프트웨어 설치를 전문으로 하는 `mise`라는 프로그램을 설치합니다.
(`mise`에 대한 자세한 내용은 [공식 웹사이트](https://mise.jdx.dev/)에서 볼 수 있습니다.)
`curl https://mise.run | sh` 명령은 인터넷에서 스크립트를 내려받아 실행하며 `mise`를 설치합니다.
인터넷에서 받은 스크립트를 실행하는 일은 위험할 수 있습니다.
누군가 스크립트에 악성 명령을 넣어 둘 수도 있기 때문입니다.
하지만 스크립트를 내려받는 사이트를 신뢰한다면 편리한 방법입니다.

두 번째 명령은 `mise`를 실행해 Jujutsu를 임시 디렉터리에 내려받습니다.
이 시점에는 `~/.local/bin`이 `PATH`에 들어 있는지 확신할 수 없으므로 `mise` 실행 파일의 전체 경로(`~/.local/bin/mise`)를 지정합니다.
(자세한 내용은 ["터미널 기초" 장](./terminal_basics.md#the-path-variable)을 참고하세요.)
`mise`가 운영체제와 CPU 아키텍처에 맞는 바이너리를 알아서 가져옵니다.

이후 명령은 내려받은 바이너리를 사용자용 프로그램이 모여 있는 `~/.local/bin`으로 옮깁니다.
`rm -rf /tmp/jj-install`(remove recursive force)는 임시 다운로드 디렉터리와 그 안의 내용을 삭제합니다.

마지막으로 `exec $SHELL --login`은 셸을 재시작해 시작 스크립트를 다시 실행하게 합니다.
Ubuntu 같은 일부 리눅스 배포판은 터미널이 시작될 때 해당 디렉터리가 존재할 경우에만 `~/.local/bin`을 `PATH`에 추가합니다.
따라서 Jujutsu 설치 후 터미널을 재시작하면 새 프로그램을 찾을 수 있게 만드는 간단한 방법입니다.

혹시 **아예** `~/.local/bin`을 `PATH`에 추가하지 않는 배포판도 있을 수 있습니다.
그럴 경우 위 명령이 동작하지 않습니다.
저는 그런 배포판을 모르지만 (관련 사례를 알고 있다면 [이슈를 열어](https://github.com/jj-for-everyone/jj-for-everyone.github.io/issues/new) 알려 주세요!)
그럴 땐 [셸 시작 스크립트](./terminal_basics.md#startup-scripts)에서 `PATH` 변수를 직접 확장하면 됩니다.
```

````admonish info title="기타 설치 방법" collapsible=true
다양한 플랫폼을 위한 공식 설치 방법은 [여기](https://jj-vcs.github.io/jj/latest/install-and-setup/)에 정리되어 있습니다.
제가 중요하다고 생각하는 몇 가지 방법도 함께 소개합니다.

[cargo-binstall](https://github.com/cargo-bins/cargo-binstall)을 사용한다면 다음 명령이 잘 동작합니다.

```sh
cargo-binstall jj-cli
```

Mac과 Homebrew 사용자라면 다음 명령을 쓰세요.

```sh
brew install jj
```

Rust 툴체인이 설치되어 있고 소스에서 직접 컴파일하고 싶다면 아래를 실행하세요.

```sh
cargo install --locked --bin jj jj-cli
```

Jujutsu의 [릴리스 페이지](https://github.com/jj-vcs/jj/releases/latest)에서 바이너리를 직접 내려받을 수도 있습니다.
"Assets"까지 스크롤하면 다운로드 가능한 아카이브 목록이 있습니다.
운영체제와 CPU 아키텍처 두 가지 요소에 따라 올바른 파일이 달라집니다.
파일 이름에서 자신의 시스템과 일치하는 문자열을 찾으세요.

운영체제 식별 방법:

| 운영체제 | 찾을 문자열 |
| --- | --- |
| Linux | unknown-linux-musl |
| Mac | apple-darwin |
| Windows | pc-windows-msvc |

CPU 아키텍처 식별 방법:

| CPU 제조사 | 찾을 문자열 |
| --- | --- |
| Intel | x86_64 |
| AMD | x86_64 |
| Apple | aarch64 |
| ARM | aarch64 |
| Qualcomm(Snapdragon) | aarch64 |

올바른 아카이브를 내려받았으면 압축을 풀어야 합니다.
파일 탐색기에서 아카이브를 우클릭해 "Extract" 같은 메뉴를 선택하면 됩니다.
압축을 풀면 문서와 "jj"라는 파일이 들어 있습니다.
이를 `~/.local/bin/` 디렉터리로 옮기세요.
(프로그램을 따로 모아 두는 위치가 있다면 그곳을 사용해도 됩니다.)
````

## 초기 설정

Jujutsu는 설정 옵션이 매우 많지만 지금은 대부분을 신경 쓰지 않아도 됩니다.
**반드시** 설정해야 하는 것은 이름과 이메일뿐입니다.
필수 메타데이터이며, 이 정보가 없으면 일부 기능이 제대로 동작하지 않습니다.
물론 저장소에 실제 이름과 이메일을 남기고 싶지 않다면 가명을 써도 됩니다.

학교나 회사 프로젝트를 진행한다면 실명과 학교/회사 이메일을 써도 문제 없습니다.
이런 저장소는 보통 외부에 공개되지 않습니다.

누구나 볼 수 있는 오픈 소스 프로젝트를 다룬다면 더 신중해야 할 수도 있습니다.
이름은 GitHub 핸들을 사용해도 되고, 실명을 쓰는 사람도 많습니다.
이메일은 더 민감합니다.
개인 이메일을 사용하면 스팸을 받을 위험이 있습니다.
오픈 소스 전용 이메일을 만드는 방법도 있고, GitHub이 제공하는 주소를 쓰는 방법도 있습니다.
이 주소는 GitHub 계정을 식별하지만 메일을 받을 수는 없습니다.
[GitHub 이메일 설정](https://github.com/settings/emails)에서 "Keep my email address private"를 선택하면 개인용 주소가 상단에 표시됩니다.

사용자 이름과 이메일을 설정하는 명령은 다음과 같습니다.

```sh
jj config set --user user.name "Anonymous"
jj config set --user user.email "anon@local"
```

셸 자동 완성을 원한다면 [이 문서](https://jj-vcs.github.io/jj/latest/install-and-setup/#command-line-completion)를 참고하세요.
"셸 자동 완성"이 무엇인지 모른다면 걱정하지 마세요. 지금은 중요하지 않습니다.

## 간단한 텍스트 편집기 설치

Jujutsu는 가끔 텍스트 파일 수정을 요구합니다.
기본 텍스트 편집기는 Linux와 Mac에서 `nano`입니다.
잘 동작하지만 처음 접하는 사람에게 직관적이지 않을 수 있습니다.
(<kbd>Ctrl+O</kbd>가 저장, <kbd>Ctrl+X</kbd>가 종료입니다.)

선택 사항이지만 [edit](https://github.com/microsoft/edit)라는 텍스트 편집기를 설치하길 권장합니다.
제가 보기엔 가장 단순하고 직관적인 대안입니다.
위에서 추천한 대로 `mise`로 Jujutsu를 설치했다면 같은 방법으로 `edit`도 설치할 수 있습니다.

```sh
mise install-into edit@latest /tmp/edit-install
mv /tmp/edit-install/edit ~/.local/bin
rm -rf /tmp/edit-install
```

다른 방법으로 Jujutsu를 설치했다면 `edit`도 알아서 설치하세요.

다음으로 Jujutsu가 텍스트 파일을 열 때 `edit`를 사용하도록 설정해야 합니다.

```sh
jj config set --user ui.editor edit
```

앞으로 Jujutsu가 텍스트 파일을 열면 `edit`로 실행합니다.
편집을 마치면 메뉴 바에서 "File" → "Exit"를 클릭하거나 <kbd>Ctrl+Q</kbd>로 편집기를 종료하세요.
파일을 저장할지 묻는 창이 뜨면 <kbd>Enter</kbd>로 확인하면 됩니다.
끝입니다!
이 편집기를 처음 사용할 때 다시 한 번 상기해 드리겠습니다.
