## @RequestMapping

- @GetMapping
- @PostMapping
- @DeleteMapping
- @PutMapping
- @PatchMapping

### 특정 HTTP 메소드 요청만 허용하기

```java
@GetMapping(value = "/test")
// @RequestMapping (value = "/test", method = RequestMethod.GET)
public String mappingGetV2(){
    log.info("mapping-get-v2");
    return"ok";
}
```

### PathVariable 경로 변수 사용하기

```java
@GetMapping(value = "/mapping/{userid}")
public String mappingPath(@PathVariable("userid") String data){
    log.info("mappingPath userId={}",data);
    return"ok";
}
```

### 매핑 시 헤더에 특정 조건 넣기

```java
@GetMapping(value = "/mapping-param", params = "mode=debug")
public String mappingParam(){
    log.info("mappingParam");
    return"ok";
}
```

### 매핑 시 특정 파라미터를 조건으로 넣기

```java
@GetMapping(value = "/mapping-header", params = "mode")
public String mappingHeader(){
    log.info("mappingHeader");
    return"ok";
}
```
- `params="mode"`: mode 파라미터 포함하는 경우
- `params="!mode"`: mode 파라미터 미포함인 경우
- `params="mode=debug"`: mode 값은 debug인 경우
- `params="mode!=debug"`: mode 값이 debug 아닌 경우
- `params={"mode=debug","data=good"}`: mode 값이 debug이고 data 값이 good인 경우



### 미디어 타입에 조건 추가해 매핑하기

```java
@PostMapping(value = "/mapping-consume", consumes = "application/json")
public String mappingConsumes(){
    log.info("mappingConsumes");
    return"ok";
}
```