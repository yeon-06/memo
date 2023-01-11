### `@Entity`란?

- JPA가 관리하는 클래스
- 테이블과 매핑되는 클래스
- public 또는 protected 기본 생성자 필수
  - 기본 생성자가 없는데 돌아가는 경우 👉 https://www.inflearn.com/questions/105043
- final, enum, interface, inner 클래스 사용 시 @Entity로 매핑 불가능
- 값을 저장할 필드에 final 사용 불가

### DB 스키마 자동 설정

> persistence.xml 설정의 일부

```xml
<property name="hibernate.hbm2ddl.auto" value="create"/>
```

- `create`: 기존 테이블 삭제 후 생성
- `create-drop`: create와 같으나 종료 시점에 테이블 삭제
- `update`: 변경 사항만 반영
- `validate`: Entity와 Table 정상 매핑 여부만 확인
- `none`: 사용 X

### 필드와 컬럼 매핑

- `@Column` : 컬럼 매핑
- `@Temporal` : 날짜 타입 매핑 (LocalDate 사용 시 생략 가능)
- `@Enumerated` : enum 타입 매핑
- `@Lob` : BLOB, CLOB 매핑
- `@Transient` : 매핑 무시

### 기본키

- `@Id` 사용
- `@GeneratedValue` 자동 생성
    - IDENTITY: DB에 위임
    - SEQUENCE: DB 시퀀스 오브젝트 사용
    - TABLE: 키 생성용 테이블 생성해 DB 시퀀 스 흉내
    - AUTO: 방언에 따라 자동 지정 (default)

> null이 아니고, 유일하고, 변경되면 안된다.
