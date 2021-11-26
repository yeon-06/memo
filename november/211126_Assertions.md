# Assertions
> [junit 공식 문서](https://junit.org/junit5/docs/5.0.1/api/org/junit/jupiter/api/Assertions.html)

- junit에서 지원하는 테스트를 위한 유틸리티 메소드 모음
- 실패 시 throw AssertionFailedError


### 메소드 종류
- assertAll(): 주어진 파라미터들이 전부 실행되는지
- assertArrayEquals(): 배열 deeply 비교
- assertEquals(): 두 값 비교
- assertFalse(): 조건이 참이 아닌 경우
- assertIterableEquals(): Iterable deeply 비교
- assertLinesMatch(): List<String> 비교
- assertNotEquals(): 두 값이 다른지 비교
- assertNotNull(): null이 아닌지 비교
- assertNotSame(): 같지 않은지 비교
- assertNull(): null인지 비교
- assertSame(): 같은지 비교
- assertThrows(): throw 발생하는지
- assertTimeout(): 시간 초과 전에 실행 완료하는지
- assertTimeoutPreemptively(): 시간 초과 전에 실행 완료하는지
- assertTrue(): 조건이 참인 경우
- fail(): 테스트 실패 시키기