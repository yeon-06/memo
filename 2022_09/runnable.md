먼저 프로세스와 스레드의 차이에 대해 잘 모르는 사람들은 [이 글](https://yeonyeon.tistory.com/186)을 읽기 바란다.

Thread를 생성하는 방법으로는 아래와 같은 방법들이 있다.

1. implements Runnable
2. extends Thread

Thread 클래스를 살펴보면 Runnable을 구현했음을 확인할 수 있다.

```java
public class Thread implements Runnable { ...
}
```

Runnable 클래스를 살펴보자.
스레드 생성하는 모든 클래스는 Runnable 구현이 필수적이다.

```java

@FunctionalInterface
public interface Runnable {
    public abstract void run();
}
```

run() 메서드를 반드시 구현해야한다.
스레드 생성을 위해 Runnable 인터페이스를 구현하는 객체를 만들었다고 가정해보자.
생성된 스레드를 시작하면 기존에 실행 중이던 스레드에서 run 메서드가 호출된다.

> Oracle Docs 원문  
> When an object implementing interface Runnable is used to create a thread, starting the thread causes the object's run
> method to be called in that separately executing thread.

이를 눈으로 확인해보고 싶어서 다음과 같은 테스트 코드를 작성했다.

```java
@Test
void testRunnableThread() throws InterruptedException{
    // 하단의 RunnableThread 클래스를 Runnable 인터페이스의 구현체로 만들고 Thread 클래스를 활용하여 스레드 객체를 생성한다.
    Thread thread=new Thread(new RunnableThread("hello thread"));

    // 생성한 thread 객체를 시작한다.
    thread.start();

    // thread의 작업이 완료될 때까지 기다린다.
    thread.join();
}

private static final class RunnableThread implements Runnable {

    private String message;

    public RunnableThread(final String message) {
        this.message = message;
    }

    @Override
    public void run() {
        log.info(message);
    }
}
```

start(), join(), run() 총 3개의 디버그를 걸어놓고 호출되는 순서를 살펴보았다.
예상한 순서는 start -> run -> join이었으나 실제로 디버그가 걸린 순서는 start -> join -> run이었다.
주변에 조언을 구해보았더니 start()가 되었을 때 run()이 동작한 것은 맞으나.. 개발자가 눈으로 확인할 수 있는 시점은 join()이 호출된 후라고 한다.
그래서 스레드를 공부하는게 어렵다고 하셨다. 😭
