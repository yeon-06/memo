### 'Optional<Object클래스>' used as type for parameter '파라미터명' 경고
> 자세한 설명은 [블로그](https://yeonyeon.tistory.com/224) 를 참고 부탁드립니다.

1. 메서드에 조건부 로직을 유도한다.
2. 파라미터의 값이 3가지 경우로 들어올 수 있다. 
   - Optional을 사용 X -> null, null이 아닌 값
   - Optional을 사용 -> null, value가 null인 Optional, value가 null이 아닌 Optional
3. Optional의 cost는 비싸다. 


Java 설계자인 Brian Goetz는 Optional에 대해 아래와 같이 정의했다.
```
Optional is intended to provide a limited mechanism for library method return types where there needed to be a clear way
to represent “no result," and using null for such was overwhelmingly likely to cause errors.
```


