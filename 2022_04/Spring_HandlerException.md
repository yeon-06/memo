### @HandlerException

- API 호출 시 발생하는 예외를 처리하기 위한 어노테이션
- Controller에서 선언 시 해당 Controller에서만 동작
- @ControllerAdvice와 함께 활용하면 여러 Controller에서 동작 가능

```java

@RestController
@RequestMapping("/test")
public class TestController {
    // ... 

    // IllegalArgumentException 발생 시 동작 1
    @ExceptionHandler(IllegalArgumentException.class)
    public String handleException1() {
        return "error!";
    }

    // IllegalArgumentException 발생 시 동작 2
    @ExceptionHandler
    public String handleException2(IllegalArgumentException e) {
        return e.getMessage();
    }

    // HTTP 상태 코드 지정 1
    @ExceptionHandler
    public ResponseEntity<String> handleException3(IllegalArgumentException e) {
        return new ResponseEntity<>(e.getMessage(), HttpStatus.BAD_REQUEST);
    }

    // HTTP 상태 코드 지정 2
    @ExceptionHandler
    @ResponseStatus(HttpStatus.BAD_REQUEST)
    public ResponseEntity<String> handleException4(IllegalArgumentException e) {
        return e.getMessage();
    }

    // handleException6보다 우선 순위 높음 - IllegalArgumentException extends RuntimeException
    @ExceptionHandler(IllegalArgumentException.class)
    public String handleException5() {
        return "IllegalArgumentException!";
    }

    // handleException5보다 우선 순위 낮음 - IllegalArgumentException extends RuntimeException
    @ExceptionHandler(RuntimeException.class)
    public String handleException6() {
        return "Exception!";
    }
}
```

> 자세한 설명은 [블로그](https://yeonyeon.tistory.com/218) 를 참고해주세요