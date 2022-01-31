### char[] vs String

👉 String은 char[]을 final로 선언한 것으로 편리한 기능(메소드) 제공.

### String **str = “abcd”** vs String **str = new String(”abcd”)**

- `new 생성`: Java **Heap 영역**에 새로운 객체 형태로 생성
- `리터럴 할당` : Java Heap 메모리 내부의 **String Pool**에 생성

➕ 다만 new 키워드를 이용했어도  `intern()` 메소드를 통해 String Pool에 등록 가능

### Immutable Object

= 불변 객체

- 생성 후 상태를 변경할 수 없는 객체
- 생성자, 접근 메소드에 대해 방어 복사가 필요 없음
- 객체가 갖는 값마다 새로운 객체 필요
- ex: `String`, `Integer`, `Boolean` 등

### String vs StringBuffer vs StringBuilder

|  | String | StringBuffer | StringBuilder |
| --- | --- | --- | --- |
| 변경 가능 | 불변 | 가변 | 가변 |
| thread-safe | X | O | X |
| 문자열 추가 | + | append() | append() |