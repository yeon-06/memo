### 코틀린과 null

코틀린의 타입 시스템은 널이 될 수 있는 타입을 명시적으로 지원한다.

#### Java Code

```java
int length(String str) {
   return str.length(); 
}
```

위 자바 코드 같은 경우에는 NPE가 발생할 수 있다.

#### Kotlin Code

```kotlin
fun length(str: String) = s.length
```

위 코틀린 코드에서는 length() 메서드를 호출할 때 null 값을 넘길 수 없다.
null 값을 넘기고 싶다면 아래와 같이 `?`를 붙여야한다.

```kotlin
fun length(str: String?) = s.length
```
