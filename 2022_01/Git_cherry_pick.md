> 구체적인 설명 https://yeonyeon.tistory.com/182

### error: Your local changes to the following files would be overwritten by merge: ~ Please, commit your changes or stash them before you can merge.
👉 변경 사항들 커밋

변경 사항이 없는 경우?
👉 스테이징 영역에 올라간 파일은 없는지 체크.
(git status 명령어 이용)

<br>

### fatal: bad object 커밋해시코드
### fatal: bad revision 커밋해시코드
👉 올바른 커밋 해시 코드인지 확인
👉 해당 커밋이 존재하는 브런치 최신화

<br>

### error: a cherry-pick or revert is already in progress
- cherry-pick의 `--continue`, `--abort`, `--quit` 옵션 사용