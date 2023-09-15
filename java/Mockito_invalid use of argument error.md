## org.mockito.exceptions.misusing.InvalidUseOfMatchersException: Invalid use of argument matchers! 2 matchers expected, 1 recorded: 에러

Mockito에서 stub할 때 `raw value` 또는 `ArgumentMatchers`를 사용해야 한다.  
인자 중 하나라도 ArgumentMatchers를 사용한다면 모든 인자들은 matcher로 주어져야 한다. 

```
verify(mock).someMethod(anyInt(), anyString(), eq("third argument")); // ok
verify(mock).someMethod(anyInt(), anyString(), "third argument"); // 세번째 인자가 matcher가 아님!! 
```

> ArgumentMatchers에 대해서는 [baeldung 글](https://www.baeldung.com/mockito-argument-matchers) 참고

***
참고
- https://stackoverflow.com/questions/24468456/invalid-use-of-argument-matchers
- https://stackoverflow.com/questions/16458136/mockito-invalid-use-of-argument-matchers
- https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html#when-T-
