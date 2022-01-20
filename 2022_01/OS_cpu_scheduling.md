> [이화여대 반효경 교수님의 강의](http://www.kocw.or.kr/home/cview.do?mty=p&kemId=1226304&ar=relateCourse) 를 들으며 정리한 내용입니다.

## 프로세스
### 프로세스 관련 시스템 콜
- `fork()`: 자식 프로세스 생성 (부모 프로세스를 복제)
- `exec()`: 실행
- `wait()`: 자식이 끝날 때까지 부모를 block 상태로
- `exit()`: 종료. 할당된 자원 해제

### 프로세스 간 협력
- 독립적 프로세스; Independent Process
  - 프로세스는 각자의 주소 공간을 갖고 수행
  - 원칙적으로 하나의 프로세스는 다른 프로세스의 수행에 영향 X
- 협력 프로세스; Cooperating Process
  - IPC를 통해 하나의 프로세스가 다른 프로세스 수행에 영향 미칠 수 있음
- 프로세스 간 협력 메커니즘; IPC; InterProcess Communication

### 스케줄러; Scheduler
- `장기 스케줄러`; Job Scheduler
  - 시작 프로세스 중 어떤 것을 ready queue로 보낼지 결정
  - **프로세스에 자원을 주는** 문제
  - 멀티 프로그래밍의 degree 제어
  - 시분할 시스템에는 보통 장기 스케줄러가 없음
  - 처음 프로세스 시작될 때 메모리에 들어오도록 허락해주는 역할  
    (프로세스의 new -> ready)
- `단기 스케줄러`; CPU Scheduler
  - 어떤 프로세스를 다음 번에 running할지 결정
  - 프로세스에 CPU를 주는 문제
  - 충분히 빨라야 함
- `중기 스케줄러`; Swapper
  - 여유 공간 마련을 위해 프로세스를 통째로 메모리에서 디스크로 쫓아냄
  - **프로세스에서 자원을 뺏는** 문제
  - 멀티프로그래밍의 degree 제어

### 프로세스의 상태
> 중기 스케줄러가 추가되며 Suspended; Stopped 상태가 생겨났다.
- `Running`
- `Ready`
- `Blocked`; `Wait`; `Sleep`
  - I/O 등의 이벤트를 기다리는 상태
  - 자신이 요청한 이벤트가 만족되면 Ready 상태로
- `Suspended`; `Stopped`
  - 외부적인 이유로 프로세스의 수행이 정지된 상태
  - 프로세스는 통째로 디스크에 swap out 됨
  - 외부에서 resume 해야 Active  
    (사람이 쫓아냈으면 사람이, 운영체제가 쫓아냈으면 운영체제가 다시 resume 해줘야 함)

## CPU 스케줄링

### CPU 스케줄링이 필요한 이유
- 여러 종류의 프로세스가 섞인 경우 효율적으로 CPU를 할당하기 위함
- `I/O bound job`
  - CPU가 필요한 계산 시간 < I/O 시간
  - many short CPU bursts
- `CPU bound job`
  - 계산 위주 작업
  - few very long CPU bursts

### CPU 스케줄링이 필요한 경우
- `running` -> `blocked`
  - 강제로 뺏지 않는 nonpreemptive 
  - ex: I/O 요청하는 시스템 콜
- `running` -> `ready`
  - 할당 시간 만료로 인한 interrupt
- `blocked` -> `ready`
  - I/O 완료 후 interrupt
- `terminate`
  - 강제로 뺏지 않는 nonpreemptive 
  
### CPU 스케줄러
- `Ready` 상태 프로세스 중 CPU를 할당할 프로세스 선택

> Dispatcher  
> CPU 제어권을 CPU 스케줄러가 선택한 프로세스에게 넘김    
> 위 과정을 `context switch`라고 함

### Scheduling Criteria
> = Performance Measures; 성능 척도
- `CPU utilization`; 이용률
- `throughput`; 처리량
- `turnaround time`; 소요시간
- `waiting time`; 대기시간
- `response time`; 응답시간
  - 실행 후 첫 응답이 나올 때까지의 시간

> 이용률, 처리량을 최대화하고 소요/대기/응답 시간을 최소화해야 좋다.

### CPU 스케줄링 알고리즘
- `FCFS`; `First Come First Served`
  - 선착순
  - convoy effect: 앞에 긴 프로세스가 있으면 뒤 프로세스는 길게 대기
- `SJF`; `Shortest-Job-First`
  - CPU 가장 짧게 쓰는 프로세스 순
  - 최소 평균 대기 시간 보유
  - CPU burst time 예측 필요
  - nonpreemptive
  - preemptive
    - 현재보다 더 짧은 CPU burst time 프로세스가 나타나면 뺏어줌
    - = `SRTF`; Shortest-Remaining Time First
- `Priority Scheduling`
  - 우선 순위에 따라 (`SJF`도 일종의 `Priority Scheduling`)
  - starvation 발생 가능 (계속 기다리는 프로세스 발생)  
    👉 aging 도입으로 해결 (오래 기다린 프로세스의 우선순위 높이기)
- `HRRF`; `Highest Response Ratio First`
  - 프로세스의 응답률 계산해 응답률 큰 프로세스부터
  - 응답률 = 1 + ((준비 큐 대기 시간) / (CPU 버스트 시간))
- `RR`; `Round Robin`
  - 각 프로세스는 동일 크기의 CPU 할당 시간 갖게 해 할당 시간 끝나면 인터럽트 발생해 CPU 큐의 제일 뒤에 섬
  - 대기 시간이 프로세스 CPU 사용 시간에 비례
  - 할당 시간이 너무 길면 FCFS와 다름 없음
  - 할당 시간이 너무 짧으면 context switch의 오버헤드 ↑
  - CPU burst time이 모두 같은 경우에 사용하는건 효율성 ↓
- `Multilevel Queue`; 다단계 큐
  - CPU는 하나지만 Ready Queue가 여러개
  - `foreground queue`
    - interactive
    - 빠른 응답을 위해 RR 사용
  - `backgournd queue`
    - batch
    - long job이 많아 context switch의 오버헤드를 낮추기 위해 FCFS
  - `Fixed Priority Scheduling`
    - 모든 foreground queue를 작업 후에 background queue 작업
    - starvation 발생 가능
  - `Time slice`
    - 각 큐에 CPU를 적절한 비율로 할당
- `Multilevel Feedback Queue`
  - `Multilevel Queue`와 유사하되 Ready Queue간 이동 가능

### `Multiple Processor Scheduling`; 다중 처리기 스케줄링
- CPU 여러개 존재하는 경우
- `Homogenous Processor`
  - queue를 한줄로 만들어 프로세스가 알아서 꺼내가도록
  - 특정 프로세서에서 수행되어야 하는 프로세스 있으면 복잡해짐
- `Load Sharing`
  - 일부 프로세서에 job이 몰리지 않도록 부하 적절히 공유
  - 별개 queue 또는 공동 queue
- `SMP`; `Symmetric Multiprocessing`
  - 각 프로세서가 각자 알아서 스케쥴링 결정
- `Asymmetric Multiprocessing`
  - 하나의 프로세서가 시스템 데이터의 접근, 공유 책임
  - 나머지는 위 프로세서를 따름

### Real-Time Scheduling
- 데드라인이 존재할 때의 스케줄링
- `hard real-time scheduling`
  - 반드시 deadline 안에 완료해야만 함
  - online은 도착 시간을 미리 모르지만 offline은 알고 있으므로 offline 스케줄링으로 하는 경우가 많음
- `soft real-time scheduling`
  - soft real-time task는 일반 프로세스에 비해 높은 우선 순위 갖도록 함

### Thread Scheduling
- `Local scheduling`
  - 사용자 레벨 스레드의 경우 사용자 수준의 스레드 라이브러리에 의해 스케줄링 결정
- `Global scheduling`
  - 커널 레벨 스레드의 경우 커널의 단기 스케줄러가 스케줄링 결정

### Algorithme Evaluation
- Queueing Models
  - 확률 분포로 주어지는 arrival rate와 service rate를 통해 각종 performance index 값 계산
- Implementation & Measurement
  - 실제 시스템에 알고리즘 구현해 실제 작업에 대한 성능 측정
- Simulation
  - 알고리즘 모의 프로그램으로 작성 후 trace를 입력으로 해 결과 비교