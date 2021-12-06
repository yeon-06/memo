### Repository
> repository는 remote와 local로 나뉜다.

새로운 저장소 생성하기
```
$ git init
```

repository 복제 / 다운로드
```
$ git clone <url>
```
<br>

### Branch
브랜치 목록
```
$ git branch
```

브랜치 생성 (로컬에 생성됨)
```
$ git branch <브랜치명>
```

브랜치 선택 (존재하지 않는 경우 생성 후 선택)
```
$ git checkout <브랜치명>
```

remote repository의 브랜치 목록
```
$ git branch -r
```

local repository의 브랜치 목록
```
$ git branch -a
```

브랜치 삭제
```
$ git branch -d <브랜치명>
```
<br>

### Remote
remote 목록(이름, url) 조회
```
$ git remote -v
```

remote 생성
```
$ git remote add <remote명> <url>
```

remote 삭제
```
$ git remote rm <remote명>
```
<br>

### Commit & Push
> 스테이지에 올리기 -> 커밋 -> 푸시

파일 상태 확인
```
$ git status
```

스테이지에 올리기
```
$ git add .
$ git add <파일명>
```

커밋
```
$ git commit -m "커밋 메시지"
```

커밋 로그 목록 확인
```
$ git log
```

푸시
```
$ git push <remote이름> <push할 브랜치 이름>
```

이전 커밋 취소하기
```
$ git reset -soft HEAD^ -- 코드 유지
$ git reset -hard HEAD^ -- 코드도 이전 커밋으로 변경
```
<br>

### Fetch & Merge (Pull)
> fetch -> merge
> pull은 fetch와 merge가 한 번에 일어난다.

변경사항 비교
```
$ git diff <브랜치명1> <브랜치명2>
```

merge: 현재 브랜치에 다른 브랜치의 수정사항 병합
```
$ git merge <브랜치명>
```

특정 커밋만 적용시키기
```
$ git cherry-pick <commit_hash_1>
```

fetch: remote repository의 변경된 사항들 다운로드
```
$ git fetch <remote명>
```

pull (=merge + fetch)
```
$ git pull
```