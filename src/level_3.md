# 레벨 3

이 레벨에서는 충돌 해결, 히스토리에서 파일 복원 같은 기본 문제 해결 능력을 익힙니다.
이 지식이 없다면 언젠가는 반드시 난관에 부딪히게 됩니다.

다음은 레벨 3 치트 시트입니다. [레벨 2 치트 시트](./level_2.md)도 함께 복습해 보세요.

````admonish info title="치트 시트"
저장소에서 가장 최근 작업을 되돌리고 다시 적용합니다
```sh
jj undo
jj redo
```
원격 북마크를 추적하여 그곳으로 푸시할 수 있게 합니다
```sh
jj bookmark track <NAME>@origin
```
커밋(및 해당 커밋을 가리키는 북마크)을 삭제합니다
```sh
jj abandon <CHANGE_ID>
```
특정 커밋(의 특정 파일) 상태를 복원합니다
```sh
jj restore [--from <CHANGE_ID>] [FILE_TO_RESTORE]
```
지저분한 워킹 카피를 나눕니다
```sh
jj commit --interactive
```
````
