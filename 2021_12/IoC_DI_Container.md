# IoC

> = Inversion of Control = 제어의 역전

- 프로그램의 흐름을 직접 제어하지 않고 외부에서 관리
- 필요한 인터페이스들을 호출하되 어떤 구현 객체를 호출하는지 알 수 없음

예를 들어 아래와 같은 코드가 존재한다고 하자.

```java
public class AppConfig {
    public MemberService memberService() {
        return new MemberServiceImpl(memberRepository());
    }

    private MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }
}
```

MemberServiceImpl은 어떤 객체가 주입될지 직접 정하지 않고  
AppConfig라는 **외부**에서 고민할 수 있게 된다.

<br>

# DI

> = Dependency Injection = 의존 주입

- 구체적인 의존 오브젝트와 이를 사용하는 클라이언트를 연결해주는 작업
- 외부에서 두 객체 간의 관계를 결정해주는 디자인 패턴

Coffee에 의존적인 Cafe를 고쳐보자.

### AS-IS

```java
public class Cafe {
    private Coffee coffee;

    public Cafe() {
        this.coffee = new Coffee();
    }

    public startProgramming() { ... }
}
```

### TO-BE

```java
public interface Drink {}
```

```java
public class Coffee implements Drink {
    private Drink drink;

    public Coffee(Drink drink) {
        this.drink = drink;
    }
}
```

```java
public class AppConfig {
    public Drink drink() {
        return new Coffee();
    }
}
```

<br>

# 컨테이너

> = IoC 컨테이너 = DI 컨테이너

- 객체를 생성, 관리하며 의존 관계를 연결해주는 것  
  (ex: 위 예제들의 AppConfig.java)

<br>

***
참고

1. inflearn -
   김영한님 [스프링 핵심 원리 기본편](www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8)
   강의
2. 망나니 개발자님 블로그 [DI](https://mangkyu.tistory.com/150)