### DTO에 Optional 쓰지 않기

> [지난 글](./Dont_use_Optionfal.md) 에 이어서 Optional을 쓰지 말아야하는 경우를 좀 더 설명해보겠다.

DTO라 하면 controller에서 @RequestBody 등을 통해 필요한 데이터를 담아오는 등의 역할을 하기도 한다. 
DTO에도 물론 null일 수도 있는 값이 존재할 수는 있다. 
하지만 그렇다고 Optional을 사용하는 건 큰 일이 될 수 있다. 
Optional은 선택이 가능한 **반환값**을 지원하기 위해 만들었다. 
필드 형식의 사용을 가정하지 않고 설계되어 Serializable 인터페이스를 구현하지 않았다. 
직렬화 / 역직렬화가 필요한 객체에서 사용하는 경우 문제가 될 수 있다.

정말정말 중요한 Java 설계자인 Brian Goetz의 Optional에 대한 정의를 다시 보자.

```
Optional is intended to provide a limited mechanism for library method return types where there needed to be a clear way
to represent “no result," and using null for such was overwhelmingly likely to cause errors.
```