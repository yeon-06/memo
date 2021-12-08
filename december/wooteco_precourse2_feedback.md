우테코 프리코스 1주차를 진행하고 받은 피드백을 정리해둔다.
> 1주차 후기: [https://yeonyeon.tistory.com/170](https://yeonyeon-tistory-com/170)  
> 1주차 소스: [https://github-com/yeon-06/java-racingcar-precourse](https://github-com/yeon-06/java-racingcar-precourse)

<br>

***
- 하드 코딩 금지


- 축약 금지


- 예외 케이스 고민하기


- 주석은 꼭 필요한 경우에만


- Java의 API 적극 활용
```java
// ex: List의 요소들 특정 문자로 이어붙이기
List<String> names = Arrays.asList("pobi", "jason");
String result = String.join(",", names);
```
<br>

- 배열 대신 Java Collection 활용
  - List, Set, Map 등의 Java Collection 자료 구조를 사용하면 다양하고 편리한 API 사용 가능
<br>

- 데이터를 꺼내기보다는 객체에 메시지 전송
  - 값을 비교하기 위해 get메소드 생성보다는 비교할 값을 파라미터로 보내 비교 결과를 알려주는 메소드 생성
```java
// AS-IS: 메인
private boolean isMaxPosition(Car car) {
    return car.getPosition() == maxDistance;
}

// TO-BE: Car 클래스 내부
private boolean isMaxPosition(int maxDistance) {
    return this.position == maxDistance;
}
```
<br>

- 필드 수 줄이기 위해 노력하기
  - 객체의 복잡도를 낮추고 버그 발생 가능성을 낮추기 위함
  - 불필요한 필드나 중복되는 필드 체크할 것


- 비즈니스 로직과 UI 로직 분리