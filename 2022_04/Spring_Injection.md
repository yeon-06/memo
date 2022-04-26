# 의존성 주입

### 생성자 주입

- final 키워드 사용 가능
- 테스트 코드 작성 용이

```java

@Controller
public class HomeController {

    private final GameService gameService;

    // Spring 4.3 이전 버전이라면 @Autowired 필요
    public HomeController(GameService gameService) {
        this.gameService = gameService;
    }
}
```

### 필드 주입

- Spring Boot 2.6 이하에서는 순환 참조의 위험이 있었음

```java

@Controller
public class HomeController {

    @Autowired
    private GameService gameService;
}
```

### 수정자 주입

```java

@Controller
public class HomeController {

    private GameService gameService;

    @Autowired
    public setService(GameService gameService) {
        this.gameService = gameService;
    }
}
```