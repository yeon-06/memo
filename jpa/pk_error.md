## java.sql.SQLSyntaxErrorException: (conn=602) Table 'DB이름.hibernate_sequence' doesn't exist 에러

Entity의 PK를 @GeneratedValue(strategy = GenerationType.AUTO)로 해두었을 때 발생.

**hibernate_sequence라는 테이블**에서 PK를 조회하는데 해당 테이블이 **존재하지 않아서** 발생한다.

1. DDL 자동 생성 설정 하기
2. GenerationType IDENTITY로 변경하기

> DDL이란?  
> Data Definition Language의 약자.  
> CREATE, ALTER, DROP, TRUNCATE 같은 데이터의 전체 골격을 결정

## java.sql.SQLException: Field 'id' doesn't have a default value 에러

테이블 생성 시 PK에 AUTO_INCREMENT 설정을 해줘야 사용 가능

***

더 자세한 설명: https://yeonyeon.tistory.com/181