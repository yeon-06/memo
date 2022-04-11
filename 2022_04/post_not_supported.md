### Request method 'POST' not supported 에러

@PostMapping, @GetMapping 어노테이션을 잘 살펴보자.

@PostMapping으로 해놓고 다른 메서드로 요청을 보냈다거나,  
Spring Security에서 csrf 토큰 설정이 잘못 되었을 수 있다.  
(나같은 경우는 csrf 토큰이 disabled 설정이 되어있어서 해당 문제는 아니었다.)

***
참고

- https://machine-does-not-lie.tistory.com/7