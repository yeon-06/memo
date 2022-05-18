### java.lang.IllegalStateException: Duplicate key 'key로 저장하려는 값' (attempted merging values ~~)

> 자세한 설명은 [블로그](https://yeonyeon.tistory.com/226) 를 참고해주세요

#### ❓ 에러 원인

- Collectors.toMap() 호출 시 중복되는 key 값이 존재

#### 💡 해결 방법

해결 방법은 크게 2가지가 있다.

1. key가 중복되지 않는 데이터 사용
2. toMap(Function, Function) 대신 toMap(Function, Function, BinaryOperator) 사용
