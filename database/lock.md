## 문제 상황

> 두번의 갱신 분실 문제; second lost updates problem 이라고도 함

- T1, T2 두 개의 트랜잭션이 동시에 진행되고 있다.
- T1과 T2에서는 DB에서 10이라는 데이터를 읽어왔다.
- T1은 데이터를 30만큼 더해 update 했다.
- T2는 데이터를 20만큼 더해 update 했다.
- DB에 최종적으로 남아있는 값은 무엇인가? 의도한 값이 남아있는가?

![image](https://user-images.githubusercontent.com/53105735/204140271-4a4720d2-4223-45ae-a9e5-86b781671026.png)

<br/>

## 낙관적 락과 비관적 락

### 낙관적 락; Optimistic Lock

- 트랜잭션 충돌이 발생하지 않는다고 낙관적으로 가정
- 잠금보다는 일종의 충돌감지에 가까움
- Entity의 버전을 통해 동시성을 제어 (=애플리케이션에서 지원)
- ex: JPA의 `@Version`

(+)
JPA의 `@Version`을 암시적 잠금이라 명명하는 경우도 있다. 
프로그램 코드상에 명시적으로 지정하지 않아도 잠금이 발생하는 것을 의미하는데 넓은 의미에서 보면 낙관적 락에 속한다고 생각한다.

### 비관적 락; Pessimistic Lock

- 실제 DB의 락을 이용해 동시성 제어
- ex: select ... for update
