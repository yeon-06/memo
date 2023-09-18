```
org.springframework.batch.item.ItemReader is an interface.
The implementing class will not be queried for annotation based listener configurations.
If using @StepScope on a @Bean method, be sure to return the implementing class so listner annotations can be used.
```

ItemReader를 JpaPagingItemReader를 이용해서 만들었다.
```java
public ItemReader itemReader() {
  // return JpaPaginItemReader
} 
```

하지만 스프링 배치 실행 과정 중에, ItemReader에는 존재하지 않는 메서드를 호출했고 에러가 발생하게 된 것.

ItemReader라는 인터페이스를 반환하는 것이 아닌, 구현체를 그대로 반환하여 해결할 수 있었음

***
참고: https://jojoldu.tistory.com/132
