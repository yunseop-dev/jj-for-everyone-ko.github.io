# 레벨 1

이 레벨에서는 일을 진행하는 데 필요한 최소한의 기술을 익힙니다.
가장 단순한 사용 사례, 즉 혼자 작업할 때만 충분합니다.
예를 들어 Git 저장소로 과제를 관리하고 제출하는 학생이라면 이 정도로 충분하죠.

아래 "치트 시트"에는 레벨 1에서 가장 중요한 명령이 담겨 있습니다.
시작하기 전에 머릿속을 예열하거나 시간이 지나 잊었을 때 참고하세요.

````admonish info title="치트 시트"
작성자 정보를 설정합니다
```sh
jj config set --user user.name "Alice"
jj config set --user user.email "alice@local"
```
저장소를 초기화합니다
```sh
jj git init <DESTINATION>
```
기존 저장소를 복제합니다
```sh
jj git clone <PATH_OR_URL> <DESTINATION>
```
만든 변경을 커밋합니다
```sh
jj commit
```
최신 커밋을 "main" 북마크로 푸시합니다
```sh
jj bookmark move main --to @-
jj git push
```
````
