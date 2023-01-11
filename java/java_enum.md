# enum
> 우테코 3주 차를 진행하며 enum을 사용하기 위해 간단히 정리해보는 시간을 갖고자 한다.

### enum이란?
> enumerance type = 열거형

- JDK 1.5부터 생겨난 기능으로 열거체를 정의할 수 있는 클래스
- 비교 시 실제 값 뿐만 아니라 타입까지 체크 가능
- 상수값이 재정의 되어도 다시 컴파일 할 필요 X

### 사용 방법

```java
enum Color {
    RED, YELLOW, GREEN, BLUE
}
```

기본적으로 위와 같이 정의하고 `Color.RED`와 같이 사용한다.  
아래와 같이 특정 값을 저장할 수도 있다.

```java
enum Color {
    RED(3), YELLOW(21), GREEN(5), BLUE(1);

    private final int value;

    Rainbow(int value) {
        this.value = value;
    }

    public int getValue() {
        return value;
    }
}
```

### 메소드
- `static E values()`: 해당 열거체의 모든 상수를 저장한 배열을 생성하여 반환
- `static E valueOf(String name)`: 전달된 문자열과 일치하는 해당 열거체의 상수를 반환함
- `protected void finalize()`: 해당 Enum 클래스가 final 메소드를 가질 수 없게 함
- `String name()`: 해당 열거체 상수의 이름 반환
- `int ordinal()`: 해당 열거체 상수가 열거체 정의에서 정의된 순서 반환
- `boolean equals(Object other)`: 객체가 해당 열거체 상수와 동일하면 true

> **+**  
> name() 메소드가 존재하나 모든 프로그래머들은 toString()이라는 메소드가 더 익숙할 것이다.  
> Java에서도 name()보다는 toString()이라는 메소드를 사용하기를 권장하고 있다.

### enum으로 Singleton 유지하기
Singleton이란 한 JVM에 하나의 인스턴스만 존재하는 클래스이다.  
멀티 스레드에 의해 클래스의 같은 인스턴스가 재사용된다.  

enum이 Singleton이 보장되는 이유는 크게 아래 3가지가 있다.

#### 1. clone 미지원
enum의 `clone()`이라는 메소드를 살펴보면 아래와 같다.

```java
/* Throws CloneNotSupportedException.
 * This guarantees that enums are never cloned, which is necessary to preserve their "singleton" status.
 * Returns: (never returns)
 */
protected final Object clone() throws CloneNotSupportedException {
    throw new CloneNotSupportedException();
}
```

사람들이 일반적으로 `clone()` 메소드를 이용할 때, 값만 같고 서로 다른 객체가 반환되기를 기대한다.  
enum은 **각 인스턴스의 값이 하나씩만 존재**해야 하므로 clone을 지원하지 않는다.
<br>

#### 2. 역직렬화로 인한 중복 인스턴스 생성 방지

enum은 기본적으로 `serializable`가 가능하다.  
`serializable interface`를 구현할 필요 없으므로 역직렬화 시 새로운 객체가 생성될 걱정을 안해도 된다.
<br>

#### 3. Reflection을 이용한 enum의 인스턴스화를 금지  

Enum의 생성자는 Sole Constructor이다.  
컴파일러에서 사용하고 사용자가 직접 호출할 수는 없다.
따라서 enum -> getConstructor -> newInstance로 사용하는 객체 생성 흐름이 적용되지 않는다.  
(Reclection은 new와 동일하게 클래스 내 생성자로 인스턴스를 사용하기 때문에...)

***
참고
1. [tcp 스쿨](http://www.tcpschool.com/java/java_api_enum)
2. [docs.oracle.com](https://docs.oracle.com/javase/9/docs/api/java/lang/Enum.html)
3. [stackoverflow - why are Java enums not clonable?](https://stackoverflow.com/questions/1803503/why-are-java-enums-not-clonable)
4. [Java Singleton Using Enum](https://dzone.com/articles/java-singletons-using-enum)
