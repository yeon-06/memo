# 깃 레포지토리 합치기
> 여기저기 흩어진 레포지토리를 한 레포지토리로 합치기 위해 subtree를 이용하였다.
> 보다 자세한 설명은 [블로그](https://yeonyeon.tistory.com/169) 참고

<br>

### 1. 새로운 repository 생성 (부모)
### 2. Local에 1 연결
```
$ git init          #깃 초기화 
$ git clone <url>   #부모 레포지토리 클론
```
### 3. Remote
```
$ git remote add <리모트명> <레포지토리 url>
$ git fetch <remote명> <브랜치명>
```
### 4. Subtree
```
$ git subtree add --prefix=<저장할 폴더명> <자식 레포지토리의 remote명> <부모 레포지토리의 브랜치>
```
### 5. Push
```
$ git push
```