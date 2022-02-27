## EnumMap이란? 요약본
> 전체 글: https://yeonyeon.tistory.com/195  
> Enum이란: https://yeonyeon.tistory.com/171

- Enum 타입만 key로 사용 가능한 특별한 Map
- Array를 이용하기 때문에 성능적으로 우수
  - 생성자 호출 시 `private transient K[] keyUniverse;`, `private transient Object[] vals;`에 정보 저장
- 해싱 과정이 필요 없어 HashMap보다 빠름
- null을 key로 넣는 경우 `NullPointerException` 발생
- thread-safe하지 않음
  - `Collections.synchronizedMap(EnumMap)` 하면 thread-safe함

### 사용 이유
- 성능 우수
  - 배열 사용
  - HashMap의 hash collision 고려하지 않아도 됨
- key의 제한
  - null 불가
  - Enum 타입 외 불가

