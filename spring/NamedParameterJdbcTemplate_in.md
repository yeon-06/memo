Spring은 다양한 종류의 JdbcTemplate을 지원하는데 개인적으로는 NamedParameterJdbcTemplate를 애용하는 편이다. 
NamedParameterJdbcTemplate에서는 아래 예제처럼 WHERE ~ IN (~)을 편하게 사용할 수 있다.

```java
public List<ProductEntity> findByIds(List<Long> productIds) {
    final String query = "SELECT id, name, price, image_url FROM product WHERE id IN (:productIds)";
    SqlParameterSource source = new MapSqlParameterSource("productIds", productIds);
    return jdbcTemplate.query(query, source, ROW_MAPPER);
}
```
 
여기서 **BadSqlGrammarException**가 발생하는 현상이 발견되었다.
확인해보니 productIds가 빈 값으로 들어오는 경우에는 IN () 안에 아무런 값도 들어가지 않아 SQL 문법 오류가 발생한다. 
다양한 해결 방법이 있겠지만 데이터가 없는 경우에는 빈 배열을 반환해야 한다고 생각했다. 
아래와 같이 list에 대한 검증 코드를 추가해주었다.

```java
public List<ProductEntity> findByIds(List<Long> productIds) {
    if (productIds.isEmpty()) {
        return new ArrayList<>();
    }

    final String query = "SELECT id, name, price, image_url FROM product WHERE id IN (:productIds)";
    SqlParameterSource source = new MapSqlParameterSource("productIds", productIds);
    return jdbcTemplate.query(query, source, ROW_MAPPER);
}
```
