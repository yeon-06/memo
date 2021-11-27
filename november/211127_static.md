# static
> 이전에 [static과 synchronized에 대해](https://yeonyeon.tistory.com/113) 포스트한 적이 있는데 간만에 코딩하니 개념이 헷갈렸다. 리마인드를 위해 TIL으로 작성한다.

- 메모리에 한 번 할당되며 프로그램 종료 시 해제
- Garbage Colletor가 관여하지 않는 영역의 메모리에 저장됨
- 객체 지향적이지 않아서 Java에서는 사용 지양을 권장
- interface 구현에 사용할 수 없어 재사용성이 떨어짐
- multi-thread 환경에서도 공유됨


### static과 메모리
![출처: https://mangkyu.tistory.com/47](../images/static.jpg)

JVM의 메모리 영역은 크게 `static`, `heap`, `stack` 영역으로 나뉜다.

간단한 설명을 위해 `static`과 `heap` 영역에 대해서만 말하자면  
`static` 영역은 프로그램 종료 시까지 메모리가 할당된 채로 존재한다.  
`heap` 영역은 Garbage Collector를 통해 수시로 관리 받는다.

보통 Class를 생성하면 `static`에, new 연산자를 통해 생성한 객체는 `heap` 영역에 저장된다.  

👉 static을 너무 남발하면 메모리가 할당된 채로 존재해 메모리 낭비가 된다.

### 그렇다면 static을 언제 사용하면 좋을까?
설정 파일 정보, 자주 사용하고 절대 변하지 않는 변수 등에 사용한다.  
👉 이 경우 static final 키워드를 사용하면 좋다.

자주 사용하는 메소드에 대해서도 static으로 선언하면 좋다고 하는데 이에 대해는 논해볼 여지가 있다.  
100000번이 호출되는 메소드가 있다고 하자. 이 경우 static을 통해 미리 할당해두면 좋지 않을까?  
static을 선언하면 100000번의 호출 후에도 계속 메모리에 할당된 상태이고  
선언하지 않으면 100000번의 호출 후에 인스턴스가 해제되므로 메모리 상으로는 절약이 가능하다.  
👉 어떤 것이 정답이다라고 말하기보다는 상황에 따라 선택하는 것이 옳다고 생각한다.

### 공유되는 static
static의 특성 중 `multi-thread 환경에서도 공유됨`을 주목할 필요가 있다.

```java
public class Visitor {
    static int visitCnt = 0;
    Visitor() {
        this.visitCnt++;
        System.out.print(this.visitCnt+" ");
    }

    public static void main(String[] args) {
        Visitor v1 = new Visitor();
        Visitor v2 = new Visitor();
        Visitor v3 = new Visitor();
    }
}
```

Visitor 객체를 생성할때 visitCnt가 1씩 증가하는 코드를 작성하였다.  
Visitor 객체를 총 3번 생성하였는데 visitCnt는 **static**을 통해 공유되고 있으므로 출력되는 값은 `1 2 3`이 된다.  

👉 프로그램에서 공통으로 사용되는 데이터를 관리할 때 이용할 수 있으나 thread-safe하지 않으니 주의가 필요하다.