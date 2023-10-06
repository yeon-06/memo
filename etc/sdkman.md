# sdkman

- 유닉스 기반 시스템에서 여러 sdk 버전을 병렬로 관리하기 위한 도구
- https://sdkman.io/

### install

```
$ curl -s "https://get.sdkman.io" | bash
$ source "$HOME/.sdkman/bin/sdkman-init.sh"
```

### java install

1. java list 조회
```
$ sdk list java
```

2. java 설치
```
$ sdk install java 11.0.16-tem
```

3. (선택) default 설정
```
$ sdk default java 11.0.16-tem
```
