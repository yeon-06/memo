# io.mockk.MockKException: Missing calls inside verify { ... } block.

### 문제 상황

- Kotest 사용 중에 위와 같은 예외가 발생하였음
- verify를 통해 모킹된 객체의 메서드가 호출되었는지 확인하는 상황

<br/>

### 문제 원인 & 해결

메서드를 호출하고자 하였으나 해당 객체가 모킹된 객체이기 때문에 every 등을 통해 메서드에 대한 처리를 해주어야 한다.
