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

#### Java는 Call By Value
Java에서 List나 사용자가 정의한 클래스 객체를 파라미터로 넘기면 원본 값도 변경된다.  
이 부분에서 Call By Reference라고 착각할 수 있지만 Heap Memory 영역에 생성된 객체의 '주소'를 참조하기 때문에 Call By Value이다.

## 접근 제어자
> 제어자란?  
> 클래스, 변수, 메소드 등의 선언부에 함께 사용되어 부가적인 의미를 부여

private
- 해당 클래스에서만 작동

default
- 해당 패키지에서 작동

protected
- 동일 패키지 내의 클래스 또는 이 클래스를 상속받은 다른 패키지의 클래스

public
- 접근 제한 X

## 기타 제어자

static
- 하나의 변수를 모든 인스턴스가 공유
- 메모리에 한 번 할당되며 프로그램 종료 시 해제
- interface 구현에 사용 불가능 -> 재사용성 ↓

final
- 재할당을 불가능하게 함
- 메소드 -> 오버라이딩 불가
- 클래스 -> 자신을 확장하는 자손 클래스 정의

synchronized
- 스레드 동기화 문제를 해결해 thread-safe를 지원하는 키워드
- 여러 스레드가 하나의 공유 자원에 접근할 때, 현재 데이터를 사용하는 스레드를 제외한 스레드들은 데이터에 접근하지 못하게 함
- 무분별한 동기화는 프로그램의 성능 저하를 일으킴

abstract
- 메소드의 선언부만 작성하고 실제 수행내용은 구현하지 않는 추상 메소드

#### abstract vs interface
abstract
- abstract class를 상속 받는 자식 클래스들 간에 공통 기능을 구현하고 상속 받을 때 기능을 확장시킴
- Java는 다중 상속을 지원하지 않기 때문에 abstract class만 사용하는건 한계가 존재  
  (ex: 컴퓨터는 '게임기'일 수도 있고 '개발 도구'일 수도 있지만 '게임기'와 '개발 도구'를 동시에 상속받는 것이 Java에서는 불가능.)

interface
- 상속 관계에 얽메이지 않고 공통 기능이 필요할 때 사용
- abstract method를 정의해놓고 구현하는 클래스 각 기능들을 overriding (다형성)

...

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

## Compiler vs Interpreter

Compiler
- 고급 언어로 작성된 프로그램 전체를 목적 프로그램으로 번역 -> 컴퓨터에서 실행 가능한 실행 프로그램 생성
- 번역 시간이 오래 걸리지만 한번 번역한 후에는 재번역의 필요가 없으므로 실행 속도 빠름
- 실행 파일을 위한 메모리 필요
- ex: Java, C, ...

Interpreter
- 고급 언어로 작성된 프로그램을 한줄 단위로 번역해 즉시 실행
- 목적 프로그램의 생성이 없음
- 시분할 시스템에 유용, 원시 프로그램의 변화에 대한 반응 빠름
- 번역 속도는 빠르지만 매번 번역해야하므로 실행 속도가 느림
- ex: Python, LISP, APL, ...

#### 원시 프로그램이란?
고급 언어나 어셈블리 언어로 작성된 프로그램

## Overloading vs Overriding

Overloading

- 메소드 이름은 같으나 매개변수의 타입이나 개수 등이 다른 메소드를 만드는 것
- 다양한 상황에서 메소드가 호출될 수 있도록 함

Overriding

- 상위 클래스의 메소드를 하위 클래스에서 필요에 의해 재정의하는 것

## 1급 객체 
- 변수나 데이터에 할당 가능
- 객체의 인자로 넘길 수 있어야 함
- return 값으로 사용 가능

Java8에서 람다식과 함수형 인터페이스의 등장으로 Java에서도 적용이 가능하게 됨  
아래를 보면 Comparator interface 안에 compare()가 존재한다.
```java
public interface Comparator<T> {
    int compare(T o1, T o2);
}
```

이를 람다식으로 표현하면 아래와 같이 표현할 수 있다.
```java
Comparator<Long> comp = (Long o1, Log o2) -> o2 - o1 < 0 ? -1 : 1;
```

위 코드는 아래 코드와 동일하게 작동한다.
```java
interface CustomComparator implements Comparator {
    @Override
    public int compare(Long o1, Long o2) {
        return o2 - o1 < 0 ? -1 : 1;
    }
}
```

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
5. [gilog님 블로그 - abstract vs interface](https://velog.io/@gillog/Java-Interface-vs-Abstract-Class-%EC%A0%95%EB%A6%AC)
6. [코딩팩토리 - 컴파일러와 인터프리터](https://coding-factory.tistory.com/303)
7. [강관우님 브런치 - 함수형 인터페이스](https://brunch.co.kr/@kd4/12)
8. 