### org.springframework.web.util.NestedServletException: Request processing failed; java.lang.IllegalArgumentException:Name for argument type [java.lang.Long] not available, and parameter name information not found in class file either. 에러

parameter name information, **파라미터 이름에 대한 정보를 찾지 못하는 문제**이다.

postman으로 테스트했을 때는 문제가 없었으나 테스트 코드를 작성하니 위 에러가 발생했다.

👉 **컨트롤러에서 파라미터 이름에 대한 정보만 추가**해주면 된다.

### 예제 코드

#### Controller 수정 전

```java
@ResponseBody
@GetMapping("/users/{id}") 
public UserResponseDto myPage(@PathVariable Long id){... }
```

#### Controller 수정 후

```java
@ResponseBody
@GetMapping("/users/{id}") 
public UserResponseDto myPage(@PathVariable(name = "id") Long id){... }
```

### 참고
[stackoverflow](https://stackoverflow.com/questions/25797584/name-for-argument-type-java-lang-string-not-available-and-parameter-name-info)