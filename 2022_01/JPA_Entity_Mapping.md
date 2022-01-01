> inflearn / 김영한 / 자바 ORM 표준 JPA 프로그래밍 - 기본편  
> '엔티티 매핑'편

### @Entity
- JPA를 사용해 테이블과 매핑할 클래스
- 파라미터가 없는 기본 생성자 필수 (public, protected)
- `final`, `enum`, `interface`, `inner` 클래스 불가

### @Table
- `name`: 매핑할 테이블 이름 지정
- `catalog`: DB catalog 매핑
- `schema`: DB schema 매핑
- `uniqueConstraints`: DDL 생성 시 유니크 제약 조건 생성

> DDL이란?  
> CREATE, DROP, ALTER, TRUNCATE 같은 데이터 정의어

## JPA의 기능
### DB 스키마 자동 생성
- DDL을 애플리케이션 실행 시점에 자동으로 생성해줌
- 운영이 아닌 개발 환경에서만 사용하도록 유의  
  (운영에서 애플리케이션 실행 중에 테이블의 구조를 변경하는 것은 위험하다.)
- DDL 생성 기능은 DDL을 자동 생성할 때만 사용되고 JPA의 실행 로직에 영향이 가지 않음.

hibernate.hbm2ddl.auto 속성
- `create`: 기존 테이블 삭제 후 생성
- `create-drop`: create와 같으나 종료 시점에 테이블 삭제
- `update`: 변경 사항만 반영
- `validate`: Entity와 Table 정상 매핑 여부만 확인
- `none`: 사용 X

### 필드와 컬럼 매핑
- `@Column`: 컬럼 매핑
- `@Temporal`: 날짜 타입 매핑 (LocalDate 사용 경우 생략 가능)
- `@Enumerated`: enum 타입 매핑
- `@Lob`: BLOB, CLOB 매핑
- `@Transient`: 매핑 무시

### 기본 키 매핑
- 직접 할당: `@Id`만 사용
- 자동 생성: `@GeneratedValue`와 사용

`@GeneratedValue`의 속성
- `IDENTITY`: DB에 위임 (MySQL, PostgreSQL, SQL Server, DB2, ...)
- `SEQUENCE`: DB 시퀀스 오브젝트 사용 (Oracle, PostgreSQL, DB2, H2, ...)
- `TABLE`: 키 생성용 테이블 생성해 DB 시퀀스 흉내
- `AUTO`: 방언에 따라 자동 지정 (default)

> 추가 TIP!  
> 기본 키는 null이 아니고, 유일하고, 변하면 안된다.  
> 예를 들어 주민 등록 번호를 PK로 설정했다고 가정하자.  
> 국가 정책으로 인해 주민 번호를 DB에 저장하지 못하는 상황이 발생한다면?  
> 사용자 테이블은 PK를 변경하기만 하면 되지만 해당 테이블을 조인시킨 테이블들에는 문제가 발생한다.  
> 권장: Long + 대체키 + 키 생성 전략 사용