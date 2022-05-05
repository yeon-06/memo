### exception.printStackTrace()를 지양하자

e.printStackTrace()는 {TOMCAT_HOME}/logs/catalina.out에만 기록이 남는다.  
에러 사항에서는 유지보수를 위해서라도 직접 로그 파일을 관리하는 것이 좋다.  
Log4j나 Slf4j 같은 로깅 프레임워크를 사용하자.


***

#### 참고

- https://www.slipp.net/questions/350