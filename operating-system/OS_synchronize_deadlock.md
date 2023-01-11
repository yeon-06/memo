> [이화여대 반효경 교수님의 강의](http://www.kocw.or.kr/home/cview.do?mty=p&kemId=1226304&ar=relateCourse) 를 들으며 정리한 내용입니다.

## 동기화란?
- 임계 구역에서 프로세스나 스레드들이 순서를 갖춰 자원을 사용하게 하는 것  
  (`임계 구역`: 멀티 스레드에 의해 공유 자원이 서로 참조될 수 있는 코드의 범위)
- 한 스레드가 작업 중 다른 스레드에 의한 간섭을 받지 못하도록 막는 것
- **하나의 자원을 한 번에 하나의 스레드에서만 사용**하도록 하는 기술

### java에서 동기화 하기
- `synchronized` 키워드 사용
    - 성능 하락
- `inner static class` 이용
    - 내부에 `static class`를 생성해 내부에서 객체를 생성하도록 함
    - `static`은 메모리에 한 번 할당되며 프로그램 종료 시 해제됨
    - 일반적으로 `getInstance()`라는 이름의 메소드를 생성해 `static class`에서 생성한 객체를 반환하도록 함
    - JVM에게 클래스 로딩을 맡기며 static한 싱글톤 인스턴스를 생성해 동기화 환경 구성됨
    - 다만 `Reflection`으로 파훼가 가능
- `Enum` 사용

inner static class 예제
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

### Race Condition
#### 발생 상황
- 커널 수행 중 인터럽트 발생
  - 인터럽트는 발생 즉시 인터럽트 처리루틴 수행
  - 인터럽트 처리루틴도 커널 코드임  
    (= kernel address space 공유)
  - 👉 인터럽트에서 변경될 수 있는 데이터에 대해 인터럽트를 disable 시키고 종료 후 enable 처리


- 프로세스가 System Call을 하여 커널 모드로 수행 중인데 Context Switch 발생
  - 프로세스 A가 커널 모드로 수행 중에 CPU 소유 시간이 종료되어 프로세스 B가 할당된다면?  
    프로세스 B 역시 커널 모드로 수행해 프로세스 A가 변경한 데이터를 변경할 수도 있다.
  - 👉 커널 모드에서 수행 중일 때 CPU를 선점 X  
    (= 커널 모드에서 사용자 모드로 돌아갈 때 선점)


- 멀티 프로세스 환경에서 공유 메모리 내의 커널 데이터
  - CPU가 여러개인 상황
  - 👉 한번에 하나의 CPU만 커널에 들어갈 수 있게 하기
  - 👉 커널 내부의 각 공유 데이터에 접근할 때마다 그 데이터에 대해 lock/unlock

> System Call: 사용자 프로그램이 OS의 서비스를 받기 위해 커널 함수를 호출하는 것  

#### 해결 조건
- Mutual Exclusion; 상호 배제
    - 임계 구역에 하나의 스레드만 들어감
- Progress; 진행
    - 아무도 임계 구역에 없을 때, 임계 구역에 들어가고자 하는 프로세스가 생기면 들어가게 해줘야 함
- Bounded Wating; 유한 대기
    - 프로세스가 임계 구역에 들어가려고 요청한 후부터 요청이 허용될 때까지 다른 프로세스들이 임계 영역에 들어가는 횟수에 한계가 있어야 함

#### 해결 방법
> Race Condition: 하나의 자원을 여러 프로세스나 스레드가 접근할 때 발생할 수 있는 문제
- 명령어 하나만으로 데이터를 읽고 쓰는 작업을 atomic 하게 수행하기  
  (임계 구역 문제의 근본 원인은 데이터를 읽고 쓰는 동작을 하나의 명령어로 수행할 수 없기 때문)
- **Spin Lock**
  - 임계 구역에 진입 가능할 때까지 루프를 돌며 재시도
- **Mutex**
  - 하나의 프로세스가 공유 자원을 사용 중이면 다른 프로세스의 접근 막음 (상호 배제)
- **Semaphore**
  - 자원의 상태를 나타내는 카운터
  - 임계 구역에 지정 개수만큼 접근 가능
  - 프로세스가 자원을 사용 중이면 세마포어 값을 변경해 다른 프로세스가 접근 시 대기 상태
- **Monitor**
  - `배타 동기 Queue`: 하나의 스레드만 공유자원에 접근할 수 있도록 하는 공간
  - `조건 동기 Queue`: 진입 스레드가 block 되며 새 스레드가 접근할 수 있도록 하는 공간
  - 공유자원 접근 함수에는 최대 1개의 스레드만 진입 가능  
    나머지는 `배타 동기 Queue`에서 대기
  - `진입 스레드`가 조건 동기로 block 되면 공유 자원에 `새 스레드` 접근 가능
  - `새 스레드`는 `조건 동기로 block된 스레드`를 `notify()`를 통해 깨울 수 있음
  - `깨워진 스레드`는 `현재 스레드`가 나가면 공유 자원에 다시 접근할 수 있음

- 임계 구역의 길이가 매우 짧다면 -> Block/Wake-up보다 Busy/wait 오버헤드가 더 커질 수 있음
- 일반적으로는 Block/Wake-up 방식이 더 좋음

> semaphore: 프로그래머가 직접 동기화  
> monitor: OS가 알아서

### Bounded-Buffer Problem; Producer-Consumer Problem
- `생산자 프로세스`: 데이터를 생성해 버퍼에 넣기
- `소비자 프로세스`: 데이터를 버퍼에서 꺼내기
- 각 프로세스는 여러개 존재할 수 있다
- `생산자 프로세스`는 버퍼에 빈 공간이 있어야 데이터를 넣을 수 있고,  
  `소비자 프로세스`는 버퍼에 데이터가 존재해야 데이터를 꺼낼 수 있음
- `버퍼 안에 든 메모리 개수` 또는 `버퍼의 빈 메모리 개수`를 공유 데이터로 생성해 파악할 필요가 있음  

👉 `Counting Semaphore`, `Binary Semaphore` 이용

#### Counting Semaphore
- 도메인이 0 이상인 임의의 정수 값
- 주로 resource counting에 사용

#### Binary Semaphore
- 0 또는 1
- 주로 mutual exclusion _(lock/unlock)_ 에 사용

### Readers and Writers Problem
- 한 프로세스가 DB에 write 중일 때 다른 프로세스가 접근하면 원하지 않는 결과가 나타날 수 있음
- read는 동시에 여럿이 가능
- 👉 DB 접근 시 lock, 사용 완료 후 unlock _(비효율적)_
- 👉 `readcount`라는 공유 변수를 생성해 관리
  - `readcount` == 0 -> `Writer` 접근 가능
  - `Writer` 접근중 -> `Reader` 접근 불가
  - `readcount`는 mutex를 이용해 mutual exclusion 보장
  - 수백 수만개의 `Reader`가 접근이 종료될 때까지 `Writer`가 기다려야할 수 있음  
    -> 신호등 같이 특정 주기마다 `Reader`를 받아들이면 됨

### 데드락
- 여러 프로세스가 서로 상대방에 의해 충족될 수 있는 event를 무한히 기다리는 현상
- 👉 event의 순서를 지정해주면 된다.
> ex) `프로세스1`과 `프로세스2`는 `S`, `Q`라는 세마포어를 필요로 한다.  
> `프로세스 1`이 P(S)를 통해 `S`를 획득했다.  
> `프로세스 2`가 P(Q)를 통해 `Q`를 획득했다.  
> `프로세스 1`이 P(Q)를 통해 `Q`를 얻고자 했으나 `프로세스 2`가 이미 차지했다.  
> `프로세스 2`가 P(S)를 통해 `S`를 얻고자 했으나 `프로세스 1`이 이미 차지했다.  
> `프로세스 1`과 `프로세스 2`는 서로의 자원이 필요로 하므로 둘 다 계속 `대기 상태`에서 머무른다.  
> `S`를 먼저 얻어야 `Q`를 얻을 수 있다는 조건이 생긴다면 해결된다.

#### 발생 조건
- `Mutual Exclusion`; `상호 배제`
- `No preemption`; `비선점`: 자원을 강제로 뺏기지 않음
- `Hold and wait`; `보유 대기`: 자원을 기다릴 때 보유한 자원을 놓지 않고 계속 갖고 있음
- `Circular wait`; `순환 대기`: 자원을 기다리는 프로세스간 사이클 형성

#### 데드락 처리
- `Prevention`: 발생 조건 중 단 하나라도 불만족 시키기
- `Avoidance`: 자원 요청에 대한 부가적인 정보를 이용해 데드락 가능성 없는 경우에만 자원 할당
- `Detection and Recovery`: 발생 허용하되 발견 시 Recovery 작업
  - Detection
    - 자원당 단일 인스턴스: Resource-Allocation Graph 이용
    - 자원당 멀티 인스턴스: Bankers's algorithm 이용
  - Recovery
    1) Process termination
       - 모든 데드락된 프로세스 종료  
       - 데드락 순환 종료될 때까지 하나씩 프로세스 종료
    2) Resource Preemption
- `Ignorance`: 책임 X
  - 데드락은 매우 드문 상황 -> 조치가 더 큰 오버헤드 야기할 수 있음
  - UNIX, Windows 등 범용 OS에서 채택

> **Resource-Allocation Graph**  
> request edge: 프로세스가 자원 요청  
> assignment edge: 프로세스가 자원 요청할 수도 있음
> 
> 모든 edge를 고려해 cycle이 생성되면 자원 할당 X    
> cycle 생성 여부 조사: O(n^2) 