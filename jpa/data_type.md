> inflearn / 김영한 / 자바 ORM 표준 JPA 프로그래밍 - 기본편  
> Chapter '값 타입'  
> 실습 예제 Git: https://github.com/yeon-06/inflearnSpring/tree/master/jpa-ex1


JPA의 데이터 타입는 크게 Entity 타입과 값 타입으로 나뉜다.

## 엔티티 타입
- @Entity로 정의하는 객체
- 데이터 변해도 식별자로 지속 추적 가능
- 키나 데이터 값 바뀌어도 식별자로 인식 가능  
  ex: Member 엔티티의 age 값을 변경해도 식별자를 통해 인식 가능

## 값 타입
- int, Integer, String같은 단순 값으로 사용하는 자바 기본 타입이나 객체
- 식별자 없고 값만 존재해 변경 시 추적 불가
- 크게 `기본 값 타입`, `임베디드 타입`, `컬렉션 값 타입`으로 나뉨

### 기본 값 타입
- Java 기본 타입 (ex: int, double, ...)
- 래퍼 클래스 (ex: Integer, Long, ...)
- String
- 기본 타입은 항상 값을 복사  
  (ex: int a=10; int b=a; 일때 a 변경해도 b 변경 안됨. 값이 복사된다는 의미.)
- 생명주기를 Entity에 의존하므로 **절대 공유하면 안됨**  
  (ex: 회원 엔티티 삭제 시 그 안의 이름, 나이 필드도 함께 삭제됨)
- Integer같은 래퍼 클래스나 String 같은 특수 클래스는 공유가 가능한 객체이지만 변경 방법이 존재하지 않음  
  (생성자를 통해서만 값을 할당 받고 setter 메소드 미지원)

### 임베디드 타입 (=복합 값 타입)
- 새로운 값 타입을 직접 정의 가능  
  (ex: 좌표를 저장하기 위한 Position 클래스 생성)
- int, String과 같은 기본 값 타입  
  (= Entity에 생명주기 의존)
- **기본 생성자 필수**
- 재사용 용이
- 높은 응집도
- 의미 있는 메소드 생성 가능
- 객체와 테이블을 아주 세밀하게(find-grained) 매핑 가능하게 됨
- 임베디드 타입의 값이 null이면 매핑한 컬럼 값도 모두 null

#### 사용 방법
- @Embeddable: 값 타입을 생성하는 곳에 지정
- @Embedded: 값 타입을 받는 곳에 지정
- @AttributeOverride: 두번 Embedded 하고 싶을때 컬럼명 변경 가능

```java
@Entity
public class Member {
    @Id
    @GeneratedValue
    private Long id;

    @Embedded
    private Period period;
    
    // getter, setter, 생성자, ...
}
```

```java
@Embeddable
public class Period {
    private LocalDateTime startDate;
    private LocalDateTime endDate;
    // getter, setter, 생성자, ...
}
```

#### 값 타입과 불변 객체
> 값 타입은 복잡한 객체를 조금이라도 단순화하기 위해 만든 개념  
> 단순하고 안전하게 사용할 수 있어야 함

기본 타입은 값을 대입하면 값이 복사되지만,  
객체 타입은 참조 값을 직접 대입하는 것을 막을 수 없다.
임베디드 타입 같은 값 타입을 여러 Entity에서 공유하면 위험해 불변 객체로 만드는 것이 좋다.

> 값이 복사된다는 말이 이해되지 않는다면 [이 글](https://yeonyeon.tistory.com/122)을 참고하길 바란다.

불변 객체
- 생성 시점 이후 값 수정 불가능  
  (생성자로 값 설정 후 setter 미생성)
- 객체 타입을 수정할 수 없도록 만들어 부작용을 차단
- ex: Integer, String

#### 값 타입과 동등성 비교
- 동일성 비교: 인스턴스의 참조 값 비교 ==
- 동등성 비교: 인스턴스의 값 비교 equals()  
  -> 값 타입의 equals와 hashcode를 재정의해야 함

### 컬렉션 값 타입
- 값 타입을 하나 이상 저장할 때 사용
- @ElementCollection, @CollectionTable
- DB는 컬렉션을 같은 테이블에 저장이 불가능  
  (ex: USER 테이블의 TEAM컬럼에 "1, 2, 3"식으로 문자열은 저장이 되지만 {1,2,3} 같은 List의 저장 불가능)
- 값을 변경하면 추적이 어려워 삭제 후 생성하는 방식 사용
- 값 타입 컬렉션을 매핑하는 테이블은 모든 컬럼을 묶어 기본키를 구성해야 함  
  (NOT NULL + 중복 불가)
- 값 타입 컬렉션에 변경 사항 발생 시 주인 엔티티와 연관된 모든 데이터 삭제 후 값 타입 컬렉션의 현재 값 모두 다시 저장
- 실무에서는 상황에 따라 값 타입 컬렉션 대신 일대다 관계를 고려
  일대다 관계를 위한 엔티티 생성 -> 여기에 값 타입 사용  

> city, street, zipcode 모두가 기본키
```java
@Embeddable
public class Address {
    private String city;
    private String street;
    private String zipcode;
    // getter, setter, 생성자, ...
}
```

> tip!  
> 컬렉션에서 remove는 보통 equals를 이용.  
> List<Address>에서 특정 Address를 지우고 싶으면 new Address(지우려는 값들) 객체로 지우면 된다.

- 값 타입 컬렉션에 변경 사항 발생 시 주인 엔티티와 연관된 모든 데이터 삭제 후 값 타입 컬렉션의 현재 값 모두 다시 저장
- 실무에서는 상황에 따라 값 타입 컬렉션 대신 일대다 관계를 고려
  일대다 관계를 위한 엔티티 생성 -> 여기에 값 타입 사용
