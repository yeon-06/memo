> inflearn / 김영한 / 자바 ORM 표준 JPA 프로그래밍 - 기본편  
> '연관관계 매핑 기초', '다양한 연관관계 매핑' 편  
> Git: https://github.com/yeon-06/inflearnSpring/tree/master/jpa-ex1

## 연관 관계 매핑 기초

### 연관 관계가 필요한 이유?

> 객체지향 설계의 목표는 자율적인 객체들의 협력 공동체를 만드는 것이다.  
> 객체지향의 사실과 오해 / 조영호

- `테이블`: 연관된 테이블을 찾기 위해 외래키 사용
- `객체`: 연관된 객체를 찾기 위해 참조 사용

객체를 테이블에 맞추어 데이터 중심으로 모델링 시 협력 관계를 만들 수 없음.

### 연관 관계

> `@ManyToOne`, `@OneToMany`, ... 등 이용

**되도록이면 단방향 연관 관계로 설계**하는 것이 좋지만,  
필요에 따라 양방향 연관 관계를 맺어야하는 경우가 있다.

편의상 양방향 연관 관계라고 하지만 Java에서 보면 서로 다른 단방향 관계 2개를 이을 뿐이다.

예제를 한번 살펴보자.  
Team과 Member는 일대다 관계이다.  
`MEMBER` 테이블은 `team_id`라는 외래키를 갖고 있다.

#### Team.java

```java
@Entity
public class Team {
    @Id
    @GeneratedValue
    @Column(name = "team_id")
    private Long id;

    private String name;

    @OneToMany(mappedBy = "team")
    private List<Member> members = new ArrayList<>();

    // getter, setter ...
}
```

#### Member.java

```java
@Entity
public class Member {
    @Id
    @GeneratedValue
    @Column(name = "member_id")
    private Long id;

    @ManyToOne
    @JoinColumn(name = "team_id")
    private Team team;

    private String username;
    
    // getter, setter, ...
}
```

`Team`에서는 `@OneToMany(mappedBy = "연관 관계의 주인")`를 통해 `Member 목록`을 가진다.  
`Member`에서는 `@JoinColumn`을 이용해 `Team`을 가진다.

양방향 매핑에서 주의할 점은 객체의 두 관계 중 하나를 **연관 관계의 주인**으로 지정해야 한다.  
연관 관계 주인이 외래 키를 관리하고 주인이 아닌 쪽은 read 기능만 한다.

주인이 아닌 쪽은 `mappedBy` 속성을 이용한다.  
외래 키가 있는 곳을 주인으로 설정하는 것이 좋다.  
(ex) `MEMBER` 테이블은 `team_id`라는 외래키를 갖고 있다.  
-> `Member 클래스`의 `team`이 연관 관계의 주인

> (+) 양방향 매핑 시 유의할 점  
> - 값을 연관 관계의 주인에게 입력해야 한다. 
> - 순수 객체 상태를 고려해 항상 양쪽에 값을 설정하자. (메소드를 생성해두면 좋다.)  
  -> `Team`의 이름을 변경하자. Team을 직접 조회해 변경할 수도, `Member`의 `team`을 조회해 변경할 수도 있다. 
> - `toString()`, `lombok`, `JSON` 등에서 무한 루프를 조심할 것.

## 다양한 연관관계 매핑

### 다대일 (N:1)
- `@ManyToOne`
- 외래 키가 있는 쪽이 연관 관계의 주인
- 양쪽을 서로 참조하도록 개발

### 일대다 (1:N)
- `@OneToMany`
- 객체의 구조상 반대편 테이블의 외래 키 관리 (아래 예제 참고)
- `@JoinColumn`의 사용 필수  
  -> 미사용 시 테이블을 하나 추가해 조인 테이블 방식 사용
- 되도록이면 **다대일 양방향 매핑** 이용

> ex: `Team` 객체 내에 `List<Member> members` 존재.  
> `Member` 객체 내에서는 `Team`을 관리하지 않음.

### 일대일 (1:1)
- `@OneToOne`
- 주 테이블에 외래 키
- 대상 테이블에 외래 키

> 주/대상 테이블에 외래 키 예제  
> ex: `Member`와 `Locker`는 1:1 관계인 객체이다.  
> **주 테이블**에 외래 키: `Member` 내에서 `Locker locker`를 선언해 사용.  
> **대상 테이블**에 외래 키: `Locker` 내에서 `Member member`를 선언해 사용.  
> DBA 관점에서 볼 때, 1:1 관계가 1:N 관계로 변환될 수 있다면 **대상 테이블에 외래키** 구조가 (DB 관점에서) 더 유연하다.    
> Java 개발자 관점에서 볼 때, `Member`만 조회해도 `Locker` 데이터가 존재하는지 확인 가능하고 JPA 매핑이 편리하므로 **주 테이블에 외래키** 구조가 유리하다.

### 다대다 (N:M)
- `@ManyToMany`
- RDB는 정규화된 테이블 2개로 N:M 관계 표현 불가능 (연결 테이블을 추가해 1:N, N:1 관계로 풀어냄)
- 많은 한계가 존재해 거의 사용하지 않음  
  (ex1) `Member`, `Product`, `Member_Product`가 존재한다고 할 때, `Member`가 `Product`를 몇 개 주문했고 주문 날짜가 언제인지 등의 추가적인 데이터가 필요하다.  
  `Member_Product`에는 매핑 정보만 존재하고 추가적인 데이터를 추가할 수 없다.  
  (ex2) `Member`에서 `Product`와 조인해 SQL문을 작성할 경우 `Member_Product`를 거쳐야 하므로 복잡해지고 애매하다. 