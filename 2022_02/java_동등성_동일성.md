> 우테코를 진행하며 VO와 관련된 질문을 했었는데,  
> 동등성과 동일성의 개념에 대해 생각해보면 좋을 것 같다는 제안을 듣고 한번 생각해보았다.

우리는 어떠한 두 값을 비교하기 위해서는 보통 `==`을 사용한다.  
위 연산자는 모든 값에 허용되는 것이 아니라 char, int, boolean 등의 자료형에서만 사용이 가능한데 이 자료형들을 primitive 자료형이라고 한다.  
우리가 임의로 선언한 클래스나 new 연산자로 생성한 객체, String 등은 `equals` 메소드를 주로 활용한다.

- `동일성`: 두 개의 오브젝트가 완전히 같다.
- `동등성`: 두 개의 오브젝트가 같은 정보를 가지고 있다.

동일성은 `==`을 사용하고, 동일성은 `equals`를 사용한다.

비슷한 기능을 하는 것 같은데 왜 둘을 구분해두었는가에 대해 생각해보았다.  
`==`는 대상의 내용을 비교하는 것이 아니라 대상의 주소 값을 비교한다.

`equals`는 클래스마다 세부적인 내용은 다르지만 대상의 내용을 비교한다.  
필요에 따라 `equals`를 재정의해 원하는 값을 비교하도록 커스텀 하기도 한다.  
(Value Object를 선언할 때 자주 재정의 함)

재정의한 내역이 없다는 가정 하에 기본적으로 Object의 equals는 아래와 같다.
```java
public boolean equals(Object obj) {
    return (this == obj);
}
```

이렇게만 보면 ==과 별 다를 바 없어보인다.  
하나의 예제를 보이기 위해 User라는 클래스를 선언해보았다.
```java
public class User {
    private String name;

    User(String name) {
        this.name = name;
    }
}
```

이제 User를 비교해보자.
```java
@Test
public void test1() {
    User user1 = new User("test");
    User user2 = new User("test");

    assertThat(user1 == user2).isFalse();
    assertThat(user1.equals(user2)).isFalse();
}
```

결과는 어떻게 나올까?  
당연히 둘 다 false가 나온다.  
`==`는 기본적으로 주소값을 비교한다.  
User 내부의 `equals` 메소드도 따로 재정의하지 않아 Object의 `equals`를 그대로 사용한다.

만약 User에서 `equals`를 아래와 같이 재정의한다면?

```java
public class User {
    private String name;
    
    User(String name) {
        this.name = name;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        User user = (User) o;
        return name.equals(user.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name);
    }
}
```

`equals`와 `hashCode`는 IntelliJ에서 자동 완성으로 지원해주는 기능을 사용했다.  
잘 살펴보면 name이 같으면 true로 return 되도록 짜여져있다.  

그렇다면 name.equals()는 어떤 값을 비교해볼까? 한번 살펴보자.

String 클래스의 `equals`를 살펴보면 아래와 같다.  
잘 이해가지 않는 사람들을 위해 주석도 추가해보았다.

```java
public boolean equals(Object anObject) {
    if (this == anObject) { // 파라미터로 주어진 객체와 **동일**한지 비교
        return true;
    }
    if (anObject instanceof String) {   // 파라미터로 주어진 객체가 String인지 판단
        String aString = (String)anObject;
        if (coder() == aString.coder()) {   // 문자 형식 비교
            return isLatin1() ? StringLatin1.equals(value, aString.value) 
                              : StringUTF16.equals(value, aString.value); // 해당 equals를 살펴보면 글자 하나하나를 비교하는 로직 포함
        }
    }
    return false;
}
```

`동등성`, `동일성`에 대해 왜 생각해보라 하신건지 잘 몰랐는데 단어의 사용을 정확히 해야겠다는 생각이 들었다.  
객체의 취급을 **동일**하게 하기 위해 `equals`와 `hashcode` 재정의하는 것에 대해 어떻게 생각하시는지에 대해 물어봤었는데  
동일이 아니라 **동등**이라고 표현했어야 맞는 말이었던 것 같다.