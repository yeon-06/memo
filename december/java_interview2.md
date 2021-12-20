## Singleton

- 한 JVM 하나의 인스턴스만 존재할 수 있도록 보장하는 디자인 패턴.
- 고정된 메모리 영역을 얻어 하나의 인스턴스를 사용하기 때문에 메모리 낭비 방지
- 너무 많은 일을 하거나 많은 데이터를 공유  
  -> 다른 클래스의 인스턴스 간에 결합도 ↑  
  -> 단일 책임 원칙 위배

#### 싱글톤일 때, 다수의 사용자가 하나의 객체에 진입하는 경우 발생하는 문제점과 해결 방법

데이터가 공유되므로 정합성을 확인하기 힘들다.  
테스트 코드를 짜기도 어려워진다. (인스턴스를 매번 초기화하기 등의 방법 선택해야함)

가장 간단한 해결 방법은 synchronized 키워드의 사용  
-> 성능 저하 발생

inner static class를 이용한 방법

```java
public class Singleton {
    private Singleton() {
    }

    private static class LazyHolder {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return LazyHolder.INSTANCE;
    }
}
```

위와 같이 내부에 static class를 선언한다.  
내부에 선언된 클래스는 getInstance()가 호출될 때 JVM에 로드되고 인스턴스를 생성.  
클래스가 로딩되는 시점에 lock이 사용되므로 thread-safe하게 된다.

다만 위와 같은 방법도 Reflection으로 파훼가 가능하므로 Enum의 사용이 추천된다.

#### Singleton vs Static

singleton

- 사용자 요청 시 하나의 인스턴스를 생성해 재사용
- 인터페이스 구현 가능
- override 가능
- OOP를 따름

static

- 인스턴스를 만들 수 없고, 생성자도 존재하지 않음
- 인터페이스 구현 및 override 불가능
- OOP가 아닌 절차적 디자인으로 함수에 가까움

## Call By Value vs Call By Reference

Call By Value

- 값에 의한 호출
- 인자로 받은 값을 복사하여 처리
- 원래 값이 보존됨

Call By Reference

- 참조에 의한 호출
- 인자로 받은 값을 그대로 사용
- 원래 값이 변경될 수 있음

> Java는 Call By Value이다. TODO
>
>

## Java의 장단점 TODO

## Java 접근 제어자 TODO

final 키워드에 대해서 설명해주세요. 각각의 쓰임에 따라 어떻게 동작하나요?

## 데이터 타입 vs 변수

변수

- : 값을 저장할 수 있는 메모리 상의 공간

타입

- : 저장할 수 있는 값의 종류와 범위
- 기본형: boolean, char, byte, short, int, long, float, double
- 참조형: 기본형을 제외한 나머지 타입, 객체의 주소 저장

## Array vs ArrayList

Array

- 여러 데이터를 하나의 이름으로 그룹핑해서 관리하기 위한 자료구조
- index와 값의 쌍으로 구성
- 논리적 저장 순서와 물리적 저장 순서 일치
- 크기가 고정되어 있음

ArrayList

- index로 관리
- 크기를 동적임
- 요소의 타입 원시형 불가능 (객체만 가능)

## 컴파일러 vs 인터프리터 TODO

## Overloading vs Overriding

Overloading

- 메소드 이름은 같으나 매개변수의 타입이나 개수 등이 다른 메소드를 만드는 것
- 다양한 상황에서 메소드가 호출될 수 있도록 함

Overriding

- 상위 클래스의 메소드를 하위 클래스에서 필요에 의해 재정의하는 것

## 1급 객체 TODO

자료형, 자료구조

## Immutable Object

- = 불변 객체
- 객체지향에서의 불변객체: 생성 후 상태를 변경할 수 없는 객체
- 생성자, 접근 메소드에 대해 방어 복사가 필요 없음
- 멀티 스레드 환경에서 동기화 처리 없이 객체를 공유할 수 있음
- 객체가 갖는 값마다 새로운 객체가 필요

불변 객체에는 `String`, `Integer`, `Boolean` 등이 있다.  
아래 코드를 보면 값이 변경된다고 착각하기 쉬운데 실제로는 새로운 값을 가진 객체를 생성하고 그 객체를 str이 참조한다.

```java
String str="a";
        str="b";  // "b" 값을 가진 객체 생성 후 str이 참조
```

#### String의 불변성

- 문자열 객체는 재사용 가능성이 높아 같은 값일 경우 재사용하기 위해 불변성을 띄도록 설계
- 메모리 절약을 위한 캐싱 기능을 위함

#### String의 리터럴 할당 vs 객체 할당

> 문자열을 리터럴(string = "abcd")로 할당하는 것과 객체(string = new String("abcd"))로 할당하는 방식의 차이

Java Heap 메모리 안에는 String Pool이 존재한다.  
리터럴로 할당하는 경우에는 이 String Pool에 생성된다.  
new 키워드를 이용한 경우는 Java Heap 영역에 새로운 객체의 형태로 생성된다.  
다만 new 키워드를 이용했더라도 intern() 메소드를 이용하면 해당 문자열을 String Pool에 등록할 수 있다.

***

1. [conatuseus님 블로그 - Immutable Object](https://velog.io/@conatuseus/Java-Immutable-Object%EB%B6%88%EB%B3%80%EA%B0%9D%EC%B2%B4)
2. [Interview Question for Beginner](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Java)
3. [liner님 블로그 - singleton vs static](https://m.blog.naver.com/ss1511/221586516299)
4. [마이너님 블로그 - String과 new String()의 차이는?](https://tomining.tistory.com/195)
5. 
