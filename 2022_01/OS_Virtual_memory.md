## 가상 메모리
- 물리적 메모리를 고려할 필요 없이 가정한 자기 자신만의 메모리 주소 공간
- 메모리 적재 단위에 따라 `요구 페이징`, `요구 세그먼테이션 방식`으로 구현
    - `요구 세그먼테이션 방식`: 하나의 세그먼트를 여러 개의 페이지로 나누어 관리하는 페이지드 세그먼테이션 기법 사용할 때 이용

### 요구 페이징; Demand Paging
- CPU의 요청이 들어온 후에야 해당 페이지를 메모리에 적재
- 메모리 사용량 ↓
- 프로세스 전체를 메모리에 올리느라 소요되는 입출력 오버헤드 ↓
- 더 많은 프로세스 수용
- `Valid-Invalid Bit`; `유효-무효 비트`
    - 각 페이지가 메모리에 존재하는지 표시
    - 페이지 테이블의 각 항목별로 저장 (invalid로 초기화)
    - `Invalid`: 사용되지 않는 주소 영역 or 페이지가 물리적 메모리에 없음
    - 무효로 세팅되어 있으면 `page fault`라고 불림
- 페이지 부재 ↓ -> 성능 ↑

#### 페이지 부재; page fault
![page fault pocess](../images/page_fault.png)
1. CPU가 무효 페이지 접근 시 `MMU`가 페이지 부재 트랩 발생
2. CPU의 제어권 `커널 모드`로 전환
3. `페이지 부재 처리루틴` 호출
    - 유효한 접근인지 체크
    - 물리적 메모리에서 빈 프레임을 할당받기 (없으면 뺏어옴 -> Page Replacement)
    - 해당 페이지를 디스크에서 메모리로 읽기
      - 디스크 I/O 종료 전까지 프로세스는 PCU를 선점당함 (block)
      - 디스크 읽기가 끝나면 page tables entry 기록, valid-invalid bit = `valid`
      - ready queue에 프로세스 삽입
    - 이 프로세스가 CPU를 잡고 다시 running
    - 중단되었던 명령 마저 실행

### Page Replacement; 페이지 교체
- 빈 프레임이 존재하지 않을 경우 어떤 프레임을 뺏을지 결정해야 함  
  (= 메모리에 올라온 페이지 중 하나를 `swap-out`해 메모리 빈 공간 확보)
- 곧바로 사용되지 않을 페이지를 쫓아내는 것이 좋음
- 동일 페이지가 여러 번 메모리에서 쫓겨났다 돌아올 수 있음
- Page Replacement의 알고리즘은 page-fault rate의 최소화가 목적

#### Optimal Algorithm
- = MIN Algorithm; OPT Algorithm; Belady's Optimal Algorithm
- MIN (OPT): 가장 먼 미래에 참조되는 페이지를 replace
- 미래의 참조를 알고 있다는 가정 하에 만들어진 알고리즘으로 실제 사용하기는 어려움  
  -> 다만 다른 알고리즘의 성능에 대한 Upper Bound 제공

#### FIFO Algorithm
- First In First Out
- FIFO Anomaly 발생: 프레임 ↑ -> page fault ↑

#### LRU Algorithm
- Least Recently Used
- 가장 오래 전에 참조된 것을 삭제
- O(1) 가장 최근 참조만 알면 됨

#### LFU Algorithm
- Least Frequently Used
- 참조 횟수가 가장 적은 페이지 삭제
- 최저 참조 횟수가 여럿인 경우
  - 여러 페이지 중 임의 로 선정
  - 성능 향상을 위해 가장 오래 전에 참조된 페이지 삭제 가능
- 참조 시점의 최근성 반영 못함  
  (미래에 여러번 호출될 예정인데 현재까지의 참조만 판단해서 삭제될 수 있음)
- O(n) 참조 횟수 비교 필요 (heap 이용해 구현하면 O(logN))

### 캐슁 기법
TODO

### 스레싱
- 집중적으로 참조되는 페이지들의 집합을 메모리에 한꺼번에 적재하지 못해 페이지 부재율 ↑ -> CPU 이용률 ↓ 현상
1. CPU 이용률 ↓
2. OS는 프로세스 수가 너무 적다 생각해 MPD ↑
3. 각 프로세스에 할당되는 메모리 양 ↓
4. 최소한의 페이지 프레임도 할당받지 못해 페이지 부재 발생 (반복)

> MPD; Multi Programming Degree; 다중 프로그래밍 정도  
> : 메모리에 동시에 올라가 있는 프로세스 수