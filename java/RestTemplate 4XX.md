RestTemplate을 이용해 외부 API를 호출하는 경우, 4XX이나 5XX이 발생하면 예외가 발생한다.  
- HttpClientErrorException –> 4xx
- HttpServerErrorException –> xx
- UnknownHttpStatusCodeException –> HTTP status
예외 처리가 필요한 경우, 응답값에 있는 상태코드를 꺼내서 비교하는 것이 아닌 exception을 try-catch 해야한다. 

참고: https://www.baeldung.com/spring-rest-template-error-handling 
