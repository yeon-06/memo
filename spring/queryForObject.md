### org.springframework.dao.EmptyResultDataAccessException: Incorrect result size: expected 1, actual 0 에러

Spring의 JdbcTemplate를 사용하다 위 에러가 발생했다.

```java
jdbcTemplate.query(sql, paramSource, rowmapper);
jdbcTemplate.queryForObject(sql, paramSource, rowmapper);
```

query()를 실행시킬 때는 결과값이 List이기 때문에 결과가 없어도 된다.  
queryForObject()는 결과가 없는 경우 EmptyResultDataAccessException가 발생한다.

```java
// NamedParameterJdbcTemplate.class
@Override
@Nullable
public <T> T queryForObject(String sql, SqlParameterSource paramSource, RowMapper<T> rowMapper)
        throws DataAccessException {

    List<T> results = getJdbcOperations().query(getPreparedStatementCreator(sql, paramSource), rowMapper);
    return DataAccessUtils.nullableSingleResult(results);
}

// DataAccessUtils.class
@Nullable
public static <T> T nullableSingleResult(@Nullable Collection<T> results) throws IncorrectResultSizeDataAccessException {
    if (CollectionUtils.isEmpty(results)) {
        throw new EmptyResultDataAccessException(1);
    }
    if (results.size() > 1) {
        throw new IncorrectResultSizeDataAccessException(1, results.size());
    }
    return results.iterator().next();
}
```

결과가 0개라면 EmptyResultDataAccessException을,  
결과가 여러개라면 IncorrectResultSizeDataAccessException을 발생시킨다.

이를 해결하기 위해서는 queryForObject() 호출 시 try-catch로 감싸면 된다.
```java
try {
    return jdbcTemplate.queryForObject(sql, paramSource, rowmapper);
} catch (EmptyResultDataAccessException e) {
    return null;
}
```