### `@RequestParam` 은 객체로 받아올 수 없을까?

`@RequestParam`은 HTTP 요청 파라미터를 받기 위해서 사용한다.

```java
// @RequestParam 예제 코드
@DeleteMapping("/sections")
public void delete(@RequestParam Long sectionId) { ... }
```

위 예제와 같이 Long, String 등 다양한 타입으로 받아올 수 있다. 
그렇다면 dto에 받아올 수는 없을까? 라는 생각이 들었다.

```java
// dto로 받는 @RequestParam 예제 코드
@DeleteMapping("/sections")
public void delete(@RequestParam SectionInfoRequest request) { ... }
```

일단 결론부터 말하자면 안된다.
몇몇 블로그에서는 잘 돌아간다고 하던데 왜 내가 짠 코드는 안됐을까?
내가 본 블로그 글에서는 아래와 같이 어노테이션을 생략하고 있었다.

```java
@DeleteMapping("/sections")
public void delete(SectionInfoRequest request) { ... }
```

`@RequestParam`은 생략해도 사용이 가능하기 때문에 처음에는 뭐가 다른지 몰랐다.
하나하나 디버깅해보니 dto로 받아오려할 때 어노테이션이 생략되어 있으면 자동으로 `@ModelAttribute`가 붙었다.
`@RequestParam`이 아닌 `@ModelAttribute`를 사용하고 있었던 것이다.
