### record

- java 14에서 등장, 16에서 안정화된 키워드
- 객체 간에 불변 데이터를 전달하는 것을 보장하기 위해 등장

아래와 같은 객체가 있다고 가정해보자.
```java
public class Person {

    private final String name;
    private final String address;

    public Person(String name, String address) {
        this.name = name;
        this.address = address;
    }
    // getter, equals, hashCode, toString
}
```

기본적인 메서드만 선언 & 재정의했는데도 몇가지 일이 반복적으로 일어난다.
- (불변을 위해) private final 선언
- 모든 인자를 포함한 생성자 선언
- getter, equals, hashCode, toString 메서드 생성

이를 record를 통해 간편하게 만들 수 있다.

```java
public record Person (String name, String address) {}
```

여기서 조금 다른 부분은 일반적으로 getter라 하면 getName(), getAddress()라는 네이밍으로 생성되어왔다.  
record같은 경우에는 name(), address()같이 필드명과 동일하다.

인자의 개수가 다른 생성자를 만들고 싶다면 아래와 같이 만들면 된다.
```java
public record Person(String name, String address) {
    public Person(String name) {
        this(name, "Unknown");
    }
}
```
