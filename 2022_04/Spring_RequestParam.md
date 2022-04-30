## @RequestParam에서 기본 생성자가 필요한 이유

### 1. HttpMessageConverter 목록 가져오기

아래는 @RequestBody에 설명된 주석의 일부를 가져왔다.

> The body of the request is passed through an HttpMessageConverter to resolve the method argument depending on the content type of the request.

### 2. MappingJackson2HttpMessageConverter 선택

여러가지 HttpMessageConverter 중에서 적합한 Converter를 찾는다.  
Spring은 JSON의 경우 Jackson2HttpMessageConverter를 선택한다.

### 3. read() 호출

read()의 로직은 MappingJackson2HttpMessageConverter가 AbstractJackson2HttpMessageConverter에서 상속받았다.  
jackson의 ObjectMapper를 호출해 값을 반환하는 것을 볼 수 있다.

```
@Override public Object read(Type type, @Nullable Class<?> contextClass, HttpInputMessage inputMessage)
throws IOException, HttpMessageNotReadableException {
    JavaType javaType = getJavaType(type, contextClass);
    return readJavaType(javaType, inputMessage);
}

private Object readJavaType(JavaType javaType, HttpInputMessage inputMessage) throws IOException { 
    ObjectMapper objectMapper = selectObjectMapper(javaType.getRawClass(), contentType);
    // 실제 로직은 훨씬훨씬 복잡하지만 return시 ObjectMapper를 사용한다는 것만 알아두자.
    return objectMapper.readValue(inputStream, javaType);
}
```

### 4. ObjectMapper가 JSON -> Object로 변환
