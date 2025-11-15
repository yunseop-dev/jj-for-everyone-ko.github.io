# 저장소 초기화

````admonish reset title="진행 상황 초기화" collapsible=true
이 장의 시작으로 되돌리려면 다음 명령을 실행하세요.

```sh
curl https://jj-for-everyone.github.io/reset.sh | bash -s initialize
```
````

"저장소"는 Jujutsu가 모든 파일(하위 디렉터리 포함)을 추적하는 디렉터리(폴더)입니다.
보통 하나의 프로젝트가 하나의 저장소에 대응하므로, 관계없는 프로젝트의 히스토리가 서로 얽히지 않습니다.
이 튜토리얼에서는 `~/jj-tutorial/repo`를 저장소 위치로 사용합니다.
다른 곳에 만들지 마세요. 그렇지 않으면 이후에 안내하는 몇몇 명령이 동작하지 않습니다.
(홈 디렉터리가 지저분해지는 것이 싫다면 언제든 삭제하고, 튜토리얼을 이어갈 때 [reset 스크립트](./structure.md#reset-your-progress)로 되돌리면 됩니다.)

새 저장소를 초기화하는 명령은 `jj git init <DESTINATION>`입니다.
새로 만든 저장소로 작업 디렉터리를 옮기기 위해 `cd`를 사용합니다.
아래 명령을 터미널에 복사해 실행하세요.

```sh
mkdir ~/jj-tutorial
jj git init ~/jj-tutorial/repo
cd ~/jj-tutorial/repo
```

첫 번째 `jj` 명령을 살펴봅시다.
`git`은 Git 호환 기능을 담당하는 서브커맨드입니다.
그중 하나가 `init`으로, Git과 호환되는 새 저장소를 초기화합니다.

"저장소를 초기화한다"는 것은 무엇일까요?
Jujutsu가 `.git`, `.jj` 두 디렉터리를 생성한다는 뜻입니다.
여기에 버전 히스토리에 관한 모든 정보가 저장됩니다.
왜 두 개일까요?
`.git` 디렉터리는 Git과 호환되는 형식으로 핵심 데이터를 저장합니다.
`.jj` 디렉터리는 Jujutsu의 고급 기능을 가능하게 하는 추가 메타데이터를 담습니다.

```admonish warning
이 디렉터리 안의 파일은 절대 직접 조작하지 마세요!
내용은 체계적인 데이터베이스입니다.
형식을 망가뜨리면 저장소가 손상될 수 있습니다.
[원격 저장소](./remote.md) 장에서 백업의 두 번째 층을 설명합니다.
```

점으로 시작하는 파일·디렉터리는 기본적으로 숨겨져 있지만 `ls -a`로 생성 여부를 확인할 수 있습니다.

```console
$ ls -a
.git  .jj
```

이전 장에서 이름과 이메일을 설정했습니다.
그 설정은 기본적으로 모든 저장소에 적용됩니다.
하지만 예제에서는 "Alice"가 작업하다가 나중에 "Bob"이 합류해 협업을 시뮬레이션할 것입니다.
아래 명령은 이 저장소에 한해 작성자 정보를 설정합니다.
기억할 필요는 없습니다. 보통은 사용하지 않는 명령입니다.

```sh
# 이 저장소에만 적용되는 설정입니다
#             vvvvvv
jj config set --repo user.name "Alice"
jj config set --repo user.email "alice@local"

# 전역 작성자 정보를 초기화합니다
jj metaedit --update-author
```
