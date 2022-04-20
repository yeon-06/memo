JdbcTemplate의 insert는 정말 쉽다.

```java
public void insert(User user) {
    String sql = "insert into users (name, age) values (?, ?)";
    jdbcTemplate.update(sql, user.getName(), user.getAge());
}
```

하지만 MySQL의 AUTO_INCREMENT의 경우에는 좀 다르게 처리해주어야 한다.  
[KeyHolder](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/jdbc/support/KeyHolder.html)
라는 인터페이스를 이용할 수 있다.

```java
public Long insert(User user) {
    String sql = "insert into users (name, age) values (?, ?)";
    
    KeyHolder keyHolder = new GeneratedKeyHolder();
    jdbcTemplate.update(connection -> {
        PreparedStatement ps = connection.prepareStatement(sql, new String[]{"id"}); // id가 AUTO_INCREMENT되는 컬럼 
        ps.setString(1, user.getName());
        ps.setString(2, user.getAge());
        return ps;
    }, keyHolder);

    return keyHolder.getKey().longValue();
}
```

KeyHolder는 key를 찾기 위한 인터페이스다.  
일반적으로 insert문에서 AUTO_INCREMENT같이 자동으로 생성되는 key를 반환할 때 사용한다.