# ⭐ 미션

톰캣 설정 중 아래 값을 적절하게 설정하고, 해당 값으로 설정한 이유를 공유

- threads max
- max connections
- accept count

위에 대한 적정 값을 예측하기 위해 부하 테스트를 진행하기로 결정하였고, 부하 테스트 도구로는 jmeter를 사용하게 되었다.

# 💻 jmeter 설치

> 맥 기준으로 설치

```shell
$ brew update
$ brew install jmeter
```

### 플러그인 추가

[option] → [plugin manager]에서 아래 항목 설치

- 3Basic Graphs
- Custom Thread Groups

### plugin manager가 없는 경우

1. [https://jmeter-plugins.org/get/](https://jmeter-plugins.org/get/) 플러그인 다운
2. `/lib/ext` 위치에 복사
3. jmeter 재시작

# 모니터링 도구를 써야할까?

jmeter의 tps 그래프만으로는 어떤 것을 어떻게 개선해야할지 감이 안잡혔음

→ 모니터링에서 추가적으로 도움되는 정보를 얻을 수 있음

→ 원래 목적에 비해 과정이 너무 복잡해지고 필요성을 크게 느끼지 못해서 쓰지 않기로 함

# Tomcat 설정

- `max-connections`: 서버가 요청을 처리할 수 있는 Connection의 수
- `accept-count`: 추가적인 Connection을 대기
- `threads.max`: 동시 요청을 처리할 수 있는 Thread의 개수

### 디폴트 설정

- -Dserver.tomcat.max-connections=8192
- -Dserver.tomcat.accept-count=100
- -Dserver.tomcat.threads.max=200

# 참고하면 좋은 리눅스 명령어

- `top`: user cpu, kernel cpu를 확인하고 DB, WAS, WS 중 어느 지점에서 CPU를 많이 사용하고 있는지
  점검 ([top 확인 방법](https://ironmask84.tistory.com/355))
- `vmstat`: CPU, Memory, Swap, Io, System call 등의 지표를 확인 ([지표보는법](https://waspro.tistory.com/155))
