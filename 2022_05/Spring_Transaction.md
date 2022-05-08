## Spring의 트랜잭션 관리

> 자세한 설명은 [블로그](https://yeonyeon.tistory.com/223) 를 참고해주세요

### 선언적 트랜잭션 관리

- Spirng 트랜잭션 AOP를 이용하는 방법
- 과거에는 xml를 활용하기도 함
- 프로그래밍적 트랜잭션 관리에 비해 간편
- ex: `@Transactional`

```java
@Transactional
public void buy(Long money){
    userDao.loseMoney(money);
    sellerDao.gainMoney(money);
}
```

### 프로그래밍적 트랜잭션 관리

- 트랜잭션 코드를 직접 작성하는 방법
- ex: `TransactionManager`, `TransactionTemplate`

#### TransactionTemplate

데이터 접근 기술에는 JdbcTemplate, JPA 등 여러가지가 존재한다. 
이 기술이 바뀌면 트랜잭션을 사용하는 방법도 달라진다. 
Spring에서는 이러한 상황을 고려해 트랜잭션에 대한 추상화를 지원한다.
`PlatformTransactionManager` 인터페이스를 이용하면 된다. 
해당 인터페이스는 총 3가지 메서드를 제공한다.

- `getTransaction()`: 현재 `TransactionStatus`를 return
- `commit()`: 변경 내역 커밋
- `rollback()`: 변경 내역 롤백

`TransactionTemplate`은 위의 `TransactionManager`를 주입 받아 사용한다. 
해당 클래스를 이용해 개발자가 트랜잭션 시작/종료 지점을 명시적으로 결정할 수 있게 된다.
