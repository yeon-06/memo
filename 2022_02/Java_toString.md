### 문제
name = yeonLog, position = 3인 Car 객체를 아래와 같이 표현하고 싶다면, 해당 로직을 어떻게 짜야할까?
```
yeonLog : ---
```

### 문제의 코드 (👎)
> Car 내부 안에서 toString() 재정의하고 View에서 출력하기
```java
@Override
public String toString() {
    return name + " : " + getGauage();
}
```

가장 처음 위 방법을 선택했던 이유는 getter의 사용을 제한하고 싶었다.  
하지만 getter의 제한 목적은 **객체에 메시지를 보내 스스로 상태에 대한 처리 로직을 수행**하기 위해서임을 잊지 말자.

### 리팩토링 코드 (👍)
> View에서 생성하고 출력하기
```java
public static void printCarStatus(Car car) {
    System.out.println(car.getName() + " : " + getGauage(car.getPosition()));
}
```

개선된 점
- model과 view가 분리됨
- 출력 형식이 바뀔 때마다 toString()을 재정의 할 필요가 없음

### 그렇다면 toString()은?
- **간결**하면서 **이해**하기 **쉬운** 형태의 **정보**를 반환해야 함
- **주요 정보를 모두 반환**해야 함
- 모든 정보를 반환할 필요는 없음 (문자열로 표시하기 부적절한 경우가 있을 수 있음)
- 잘 구현하면 디버깅이 편리해짐

***
전문: https://yeonyeon.tistory.com/188
