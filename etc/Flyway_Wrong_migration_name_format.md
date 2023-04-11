# Flyway - Wrong migration name format

### 문제 상황

* application을 띄우려고 하니 위와 같은 에러가 발생
* 개발 중 DB 테이블을 변경할 일이 있었고, resources에 sql 파일도 생성함

### 문제 원인 및 해결 방법

* 에러명 그대로 "잘못된 형식의 이름"이기 때문에 발생
* 오류명에 ~~ 이러한 형식으로 파일명을 만들어야한다고 나타남. sql 파일명을 해당 형식에 맞추면 됨
