### ❓ org/mariadb/jdbc/Driver : Unsupported major.minor version 52.0 
👉 Java와 MariaDB 버전 맞추기 (버전 확인하는 곳)

### ❓ Driver com.mysql.cj.jdbc.Driver claims to not accept jdbcUrl
👉 해결1) application.properties에서 설정한 url에 오타 없는지 확인  
👉 해결2) localhost의 경우 아래와 같이 설정해야 함  

```
spring.datasource.url=jdbc:mysql://localhost.com:3306/DB명
```

### ❓ No session repository could be auto-configured, check your configuration (session store type is 'jdbc')
👉 application.properties에서 'spring.session.store-type' 제거

### ❓ java.sql.SQLNonTransientConnectionException: Could not connect to address=(host=XXXXXXX)(port=3306)(type=master) : Socket fail to connect to host:XXXXXXX, port:3306.
#### 예상 원인1
: DB 서비스가 종료되어 있음 또는 접속할 DB의 주소를 잘못 입력    
👉 DB가 정상적으로 구동중인지 확인

#### 예상 원인2
: 계정에 대해 접근 권한이 없음  
👉 application.properties에 적은 계정의 권한 확인

#### 예상 원인3
: MariaDB의 외부 IP 접속이 불가능 👉 50-server.conf 파일에서 bind-address를 0.0.0.0(전체 공개)로 변경  

***
### 출처
1. https://stackoverflow.com/questions/62797182/driver-com-mysql-cj-jdbc-driver-claims-to-not-accept-jdbcurl
2. https://stackoverflow.com/questions/50941891/spring-session-boot-error-no-session-repository-could-be-auto-configured-chec
3. https://tyrannocoding.tistory.com/42
4. https://www.lesstif.com/dbms/mysql-client-port-113347417.html
5. https://serverfault.com/questions/844103/why-is-mysql-connecting-through-socket-even-though-im-specifying-host-and-port
