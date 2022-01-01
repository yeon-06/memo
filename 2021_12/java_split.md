우리는 문자열을 자를 때 split() 메소드를 자주 사용한다.  
요 String의 split() 메소드를 이용하다 문제가 생겼다.
<br>

`"A,B,C,"`라는 문자열 str이 있을 때 `str.split(",")`의 결과는?
- 예상: `{"A", "B", "C", ""}`
- 실제 결과: `{"A", "B", "C"}`

<br>
우리는 흔히 split() 메소드 내의 파라미터로 정규식을 넣는다.  
그런데 파라미터를 2개 넣을수도 있다는건 이번에 처음 알았다.

```java
public String[] split(String regex, int limit)
public String[] split(String regex)
```
<br>

사실 `split(regax)`를 호출해도 split 내부 코드를 살펴보면 `split(regex, 0)`을 호출하게 되어있다.  
`limit`의 디폴트 값이 `0`인 셈이다.

<br>

그렇다면 `limit` 파라미터의 역할이 뭘까?  
바로 **패턴이 적용되는 횟수를 제어**하는 역할이다.  

- `limit`이 `0`보다 큰 경우, 패턴은 최대 `limit-1`회 적용된다.  
- `limit`이 `0`보다 작은 경우, 패턴을 최대한 많이 적용할 수 있고 배열의 크기에 제약이 없어진다.  
- `limit`이 `0`인 경우, 패턴을 최대한 많이 적용할 수 있고 배열의 크기에 제약이 없어지지만 마지막의 빈 문자열은 삭제된다.

<br>

내가 원하는 맨 마지막의 빈 문자열도 유지되길 원한다면, `limit`에 음수를 넣으면 된다.

<br>

***
참고
- [Baeldung](https://www.baeldung.com/string/split)
- [docs.oracle.com](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#split(java.lang.String,%20int))