### 여태까지 나는..

정적 팩토리 메서드를 캐싱 목적으로 사용했다.  
같은 인스턴스를 반환해야하는 경우 매번 사용하기 보다는 메모리에 한번 올려놓고 계속 재사용했다.

```java
class Test {

    private static final List<Integer> list = new ArrayList<>();

    static {
        for (int i = 0; i < 10; i++) {
            list.add(i);
        }
    }

    private Test() {
    }

    public static Test of(int number) {
        return list.get(number);
    }
}
```

### 또 다른 용도

해당 객체가 가지는 필드들을 통해서 생성할 때만 생성자를 사용하고 데이터 가공을 통해 생성 시에는 정적 팩토리 메서드를 사용하기도 함 (주관적인 개발 스타일)

정적 팩토리 메서드란 `객체 생성의 역할을 하는 클래스 메서드`라고도 한다.  
`LocalTime` 클래스의 `of()` 메서드를 가져와보았다.

```java
public class LocalTime {

    // ...

    public static LocalTime of(int hour, int minute) {
        ChronoField.HOUR_OF_DAY.checkValidValue((long) hour);
        if (minute == 0) {
            return HOURS[hour];
        } else {
            ChronoField.MINUTE_OF_HOUR.checkValidValue((long) minute);
            return new LocalTime(hour, minute, 0, 0);
        }
    }
}
```

위와 같이 사용하는 이유가 무엇일까?

1. 이름을 가질 수 있다.
2. 호출할 때마다 객체를 새로 생성할 필요가 없다. (가장 위에서 예를 들었던 Test 클래스 같이)
3. 하위 자료형 객체를 반환할 수 있다.
4. 객체 생성을 캡슐화할 수 있다.

### 네이밍 컨벤션

- `from`: 하나의 매개 변수를 받아서 객체를 생성
- `of`: 여러개의 매개 변수를 받아서 객체를 생성
- `getInstance` | `instance`: 인스턴스를 생성. 이전에 반환했던 것과 같을 수 있음.
- `newInstance` | `create`: 새로운 인스턴스를 생성
- `get[OtherType]`: 다른 타입의 인스턴스를 생성. 이전에 반환했던 것과 같을 수 있음.
- `new[OtherType]`: 다른 타입의 새로운 인스턴스를 생성.

***
참고

- https://velog.io/@ljinsk3/%EC%A0%95%EC%A0%81-%ED%8C%A9%ED%86%A0%EB%A6%AC-%EB%A9%94%EC%84%9C%EB%93%9C%EB%8A%94-%EC%99%9C-%EC%82%AC%EC%9A%A9%ED%95%A0%EA%B9%8C
- 이펙티브 자바 / item 1