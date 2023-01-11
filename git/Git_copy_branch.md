# 다른 사람 저장소의 브랜치를 내 저장소로 복사하기
> 자세한 설명은 https://yeonyeon.tistory.com/187 참고 부탁드립니다

### 1. 상대방 git 레포지토리 주소 복사

### 2. 1에 대한 remote를 추가
```
$ git remote add <리모트명> <깃허브링크>
```

### 3. 로컬 branch 생성
```
$ git checkout <브랜치명>
```

### 4. 가져오고자 하는 브랜치 pull
```
$ git pull <리모트명> <리모트의 브랜치명>
```

### 5. 내 github에 push
- IntelliJ에서 프로젝트 우클릭 - Git - Push
- push 명령어 이용  
  ```
  $ git push <리모트명> <브랜치명>
  ```
