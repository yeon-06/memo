## `.properties`를 깃허브에 올리기

properties 파일들은 중요한 설정 정보들이 포함되기 때문에 공개되면 안된다.  

이를 **숨김 처리** 하는 방법은 여러가지가 있다.
Vault, AWS에서 지원해주는 Systems Manager Parameter Store 등 여러 서비스를 활용할 수 있다.
또는 properties를 아예 깃허브에 올리지 않고 서버에 직접 수동 배포하는 방법도 있다.

이번에 해볼 것은 OS 환경 변수에 저장하고 properties에서 사용하는 방법이다.
OS 환경 변수에 저장된 값들은 properties에서 아래와 같은 형태로 가져올 수 있다.

```properties
secret.key=${SECRET_KEY}
```

OS 환경 변수를 저장하는 방법도 간단하다.
리눅스 환경이라면 아래 명령어를 통해 .bashsrc 파일에 접근해 변수를 추가해주면 된다.

```
$ vi ~/.bashsrc
```

아래 예제처럼 export 키워드를 이용해 변수를 추가해주자.

```
export SECRET_KEY='12e21.11fwq2'
```