LocalDate에는 isAfter, isBefore 날짜를 비교할 수 있는 편리한 메서드를 제공한다.  
다만 주의할 점은 인자로 주어지는 날짜와 일치하는 경우에는 false이다.  
인자로 주어지는 날짜와 동일한지 확인하기 위해서는 isEqual을 사용해야한다.

example - LocalDate.java JavaDoc

```
LocalDate a = LocalDate.of(2012, 6, 30);
LocalDate b = LocalDate.of(2012, 7, 1);
```

- a.isAfter(b) == false
- a.isAfter(a) == false
- b.isAfter(a) == true
