### 🌠 Thread Pool 종료하기
> 글 전체 보기 👉 https://yeonyeon.tistory.com/271

ExecutorService를 종료시키지 않으면 계속 다음 Task 수행을 위해 스레드가 계속 대기한다. 직접 종료시켜줘야 자원을 해제할 수 있다. 심지어는 계속 대기중인 ExecutorService 때문에 JVM이
계속 실행되어서 앱이 끝에 도달해도 완전히 중지되지 않는 현상이 발생할 수 있다. ExecutorService의 다양한 종료 메서드를 살펴보자.

- shutdown()
    - 새로운 Task 요청 거절
    - 실행 중인 모든 작업을 완료된 후에 종료
- shutdownNow()
    - 즉시 중지
    - 실행 중인 모든 스레드가 동시에 중지된다는 보장은 없음

### shutdown() vs shutdownNow()
shutdown()은 실행 중인 작업이 엄청 오래 걸리거나 무한으로 실행된다면 계속 중지되지 않을수도 있다. shutdownNow()는 즉시 중지해서 현재 작업 내역이 날아갈 위험이 있다. 이 두 가지를 절충해서 한
가지 대안으로 일정 시간 동안 기다리고 그 후에도 종료되지 않은 작업이 있다면 강제 종료 시켜버리는 방법이 있다. 이 때 awaitTermination()을 활용하면 된다. awaitTermination()는 실행
중인 모든 작업이 완료될 때까지 특정 시간 동안 대기하다가 완료되지 않은 작업들의 존재 여부에 따라 true/false를 반환한다. 이 점을 이용해 다음과 같은 코드를 짜볼 수 있다.

```java
executorService.shutdown();
try {
    if (!executorService.awaitTermination(800, TimeUnit.MILLISECONDS)) {
        executorService.shutdownNow();
    } 
} catch (InterruptedException e) {
    executorService.shutdownNow();
}
```
