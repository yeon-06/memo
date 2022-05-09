### Repository vs Dao

Repository와 Dao는 어떤 차이가 있을까?

JPA를 사용할 때는 Repository라는 키워드로 클래스를 자주 만들었지만  
Java, Spring할 때는 그럴 필요를 못느껴 Dao라는 키워드를 자주 이용했다.

오늘 한 크루가 이야기를 해서 나만의 기준이 생겼다.

Dao는 '테이블'을 포인트로 두고, Repository는 '도메인' 또는 '컬렉션'을 포인트로 둔다.

예를 들어 User 테이블과 Job 테이블이 존재한다고 하자.  
User 도메인은 아래와 같을 것이다.

```java
public class User {
  private String id;
  private String name;
  private Job job;
}
```
 
Dao는 `UserDao`와 `JobDao`로 나눌 수 있다.
User의 모든 데이터를 가져오려면 `userDao.findById()`와 `jobDao.findById()`를 호출해야 한다.  
이런 식으로 여러 dao를 호출해야만 할때 Repository로 한 계층을 더 만들어주면 Service에서 어떤 쿼리들을 호출해야할지 하나하나 확인할 필요가 없게 된다.

MVC 기준으로 역할 분리를 하자면 아래와 같다.
- Dao: DB에 어떤 방식으로 요청할지
- Repository: 데이터를 어떻게 받아올지
- Service: 어떤 로직을 실행할지
- Controller: URL과 로직 사이를 매핑
