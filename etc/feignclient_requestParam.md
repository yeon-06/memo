FeignClient에서 List형태의 RequestParam 인자가 있다고 가정해보자.

```
@GetMapping("/api/boards/search")
BoardsResponse findByIds(@RequestParam("ids") List<Long> ids);
```

별도의 설정을 하지 않았다면 아래와 같은 형식으로 호출된다.
```
/api/boards/search?ids=1&ids=2&ids=3
```

물론 문제가 발생하지는 않겠지만, url을 읽기 힘들어지고 파라미터명이 너무 길어지면 url의 최대 길이를 넘어가 일부 값이 잘리는 현상이 일어나지 않을까 걱정되었다.  
따라서 아래와 같은 형식으로 보내고 싶었다.
```
/api/boards/search?ids=1,2,3
```

위와 같이 보내려만 아래 설정을 추가하면 된다.

```
@GetMapping("/api/boards/search")
@CollectionFormat(feign.CollectionFormat.CSV)
BoardsResponse findByIds(@RequestParam("ids") List<Long> ids);
```

***
참고: https://stackoverflow.com/questions/41744542/spring-cloud-feign-client-requestparam-with-list-parameter-creates-a-wrong-requ
