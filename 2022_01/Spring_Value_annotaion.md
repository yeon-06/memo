## @Value를 통해 properties를 가져오는 경우 null이 받아오는 현상

### 추측1. properties 파일을 찾지 못했다.
👉 @Controller나 @Service를 통해 빈으로 등록되는 클래스들은 @Value를 통해 값이 가져와졌다.

### 추측2. static 키워드의 사용
@Value를 통해 값을 찾는 것보다 static을 통해 호출되는 것이 더 빠르게 이루어짐.  
static을 제외하거나 static setter 메소드를 사용해 값을 넣어줘야 함.

### 추측3. bean으로 등록된 클래스만 @Value를 사용할 수 있다.
@Component로 등록한 뒤 @Value를 가져오려 했으나 실패  
👉 util 클래스를 new를 이용해 가져오려 했기 때문에 해당 부분 수정

> 해결 완료했으나 유틸로 사용하는 클래스를 컴포넌트 등록하는 것이 올바른 방법일까?에 대한 의문 