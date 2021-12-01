우테코 프리코스 1주차를 진행하고 받은 피드백을 정리해둔다.
> 1주차 후기: [https://yeonyeon-tistory-com/165](https://yeonyeon-tistory-com/165)
> 1주차 소스: [https://github-com/yeon-06/java-baseball-precourse](https://github-com/yeon-06/java-baseball-precourse)

- 이름을 통해 의도를 드러내기
  - 연속된 숫자 덧붙이기 (a1, a2, a3, ---) 금지
  - 불용어 (Info, Data, a, an, the) 금지

- 이름 축약 금지
  - 클래스와 메소드 이름을 한 두단어로 유지하려고 노력하되 지나친 축약을 하지 말자
  - Order 클래스의 배송 메소드 -> shipOrder() (X), ship() (O)

- 공백도 코딩 컨벤션이다
  - if, for,- while문 사이의 공백 잊지 말 것

- 중복 금지

- space와 tab 혼용하지 말기
  - space 또는 tab을 혼용하지 말 것-
  - Push 또는 Pull Request 이후에 들여쓰기를 확인할 수 있음

- 의미 없는 주석 없애기
  - 변수나 메소드 이름을 통해 어떤 의도인지 드러난다면 굳이 주석이 필요 없다

- 의미 있는 커밋 메시지 작성

- 구현 중 업데이트 된 기능들이 있다면 기능 목록도 함께 업데이트 하기

- 기능 목록을 재검토하기
  - 기능 목록을 클래스나 함수 설계와 구현까지 지나치게 상세히 적을 필요 없음
  - 구현 할 기능 목록을 정리하는 데 집중
  - 예외 상황에 대해서도 정리하면 좋다

- README-md 상세히 작성하기
  - 해당 프로젝트가 어떤 프로젝트인지 꼭 작성할 것

- IDE의 코드 자동 정렬 기능 활용
  - Eclipse: Ctrl+Shift+F
  - IntelliJ: Ctrl+Alt+L

- 매직 넘버 사용 금지
  - 매직 넘버란? 프로그래밍에서 상수로 선언하지 않은 숫자 (문자열은 매직 리터럴)
  - 의미 있는 상수 (static final)을 사용하자

- 구현 순서
  - 상수, 클래스 변수 -> 인스턴스 변수 -> 생성자 -> 메소드