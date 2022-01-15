## 스케줄러; Scheduler
- 장기 스케줄러; Job Scheduler
  - 시작 프로세스 중 어떤 것을 ready queue로 보낼지 결정
  - **프로세스에 자원을 주는** 문제
  - 멀티 프로그래밍의 degree 제어
  - 시분할 시스템에는 보통 장기 스케줄러가 없음
  - 처음 프로세스 시작될 때 메모리에 들어오도록 허락해주는 역할  
    (프로세스의 new -> ready)
- 단기 스케줄러; CPU Scheduler
  - 어떤 프로세스를 다음 번에 running할지 결정
  - 프로세스에 CPU를 주는 문제
  - 충분히 빨라야 함
- 중기 스케줄러; Swapper
  - 여유 공간 마련을 위해 프로세스를 통째로 메모리에서 디스크로 쫓아냄
  - **프로세스에서 자원을 뺏는** 문제
  - 멀티프로그래밍의 degree 제어

## 프로세스의 상태
> 중기 스케줄러가 추가되며 Suspended; Stopped 상태가 생겨났다.
- Running
- Ready
- Blocked; Wait; Sleep
  - I/O 등의 이벤트를 기다리는 상태
  - 자신이 요청한 이벤트가 만족되면 Ready 상태로
- Suspended; Stopped
  - 외부적인 이유로 프로세스의 수행이 정지된 상태
  - 프로세스는 통째로 디스크에 swap out 됨
  - 외부에서 resume 해야 Active  
    (사람이 쫓아냈으면 사람이, 운영체제가 쫓아냈으면 운영체제가 다시 resume 해줘야 함)

CPU 스케줄링

FCFS; First Come First Served
- 선착순

SJF; Shortest-Job-First
- CPU 가장 짧게 쓰는 프로세스 순으로
- CPU 점유 시간이 긴 프로세스가 무한정 기다리게 될 수도 있음

RR; Round Robin
- 각 프로세스는 동일 크기의 CPU 할당 시간 갖게 해 할당 시간 끝나면 인터럽트 발생해 CPU 큐의 제일 뒤에 섬
- 대기 시간이 프로세스 CPU 사용 시간에 비례