# GitHub 사용하기(선택)

약속대로 [GitHub](https://github.com/)을 사용할 때 도움이 되는 팁을 정리했습니다.
관심 없다면 이번 장은 건너뛰어도 됩니다. 이후 내용에 영향을 주지 않습니다.

GitHub는 가장 인기 있는 Git 호스팅 서비스이지만 유일한 제공자는 아닙니다.
안타깝게도 GitHub는 프로프라이어터리(비공개) 소프트웨어입니다.
소스 코드를 읽고, 수정하고, 공유할 자유가 없다는 뜻이죠.
아래에는 오픈 소스 Git 호스팅 소프트웨어와 이를 사용하는 서비스 목록을 적었습니다.
디지털 자유를 중요하게 생각한다면 저장소를 이런 대안에 호스팅하는 것을 고려해 보세요.

- [Forgejo](https://forgejo.org/)
- [Codeberg](https://codeberg.org/)
- [Sourcehut](https://sourcehut.org/)
- [Gerrit](https://www.gerritcodereview.com/)
- [Tangled](https://tangled.sh/)
- [Radicle](https://radicle.xyz/)

## SSH 키로 인증하기

Jujutsu가 여러분 대신 커밋을 주고받으려면 GitHub 사용자로 인증해야 합니다.
아이디와 비밀번호만으로도 가능하지만, 매우 번거롭기 때문에 추천하지 않습니다.
백업 과정이 귀찮을수록 **덜 자주** 하게 됩니다.
백업이 줄어들면 작업물을 잃을 위험이 커지겠죠!
그렇다면 인증 과정을 최대한 매끄럽게 만들어야 합니다.

가장 좋은 인증 방식은 SSH 키를 사용하는 것입니다.
비밀번호보다 편리하고 안전합니다.
GitHub에는 설정 방법이 잘 정리되어 있으니 아래 문서를 따라 하세요.
- [새 SSH 키 생성](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [SSH 키를 계정에 추가](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

다음 명령으로 설정이 잘 되었는지 확인할 수 있습니다.

```sh
ssh -T git@github.com
```

예상되는 출력은 다음과 같습니다.

```
Hi user! You've successfully authenticated, but GitHub does not provide shell access.
```

## GitHub에 새 저장소 만들기

이미 존재하는 저장소를 사용할 예정이라면 이 구간을 건너뛰세요.

GitHub에서 새 저장소를 만들려면 [이 링크](https://github.com/new)를 클릭하고 폼을 작성하세요.
소유자(보통 본인 계정)와 저장소 이름만 고르면 됩니다.
공개 범위도 원하는지 확인하세요(나중에 변경 가능).

이미 로컬 저장소에 내용이 있고 이를 새 원격으로 푸시하려면, **저장소를 어떤 콘텐츠로도 초기화하지 마세요.**
템플릿, README, `.gitignore`, 라이선스를 추가하지 않는다는 뜻입니다.

마지막으로 "Create repository"를 클릭합니다.

## 기존 저장소 클론하기

브라우저에서 기존 저장소의 페이지로 이동합니다.
초록색 "Code" 버튼을 클릭하세요.
(앞에서 설명한 대로 SSH 키를 설정했다면) 드롭다운에서 **SSH** 를 선택합니다.
표시된 URL을 복사하세요.

![](./github_ssh_url.png)

마지막으로 해당 URL을 Jujutsu의 클론 명령에 붙여넣습니다.

```sh
jj git clone <COPIED_URL>
```
