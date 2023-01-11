### try-finally보다 try-with-resources 사용하기

> 좀 더 구체적인 이유는 이펙티브 자바 item 9를 참고하면 좋다.

<br/>

#### AS-IS

- PreparedStatement를 finally에서 close
- close시 SQLException이 발생할 수 있어 try-catch를 한번더 감싸줌
- 로직이 복잡함

```java
public void updateTurn(Team turn, int id) {
    String sql = "update board set turn = ? where id = ?";
    PreparedStatement preparedStatement = null;
    try {
        preparedStatement = connection.prepareStatement(sql);
        // preparedStatement 실행 로직 
    } catch (SQLException e) {
        e.printStackTrace();
    } finally {
        if (preparedStatement != null) {
            try {
                preparedStatement.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

<br/>

#### TO-BE

- try-with-resources 활용
- try가 종료되는 시점에 AutoCloseable 인터페이스의 close() 메서드가 자동 호출  
  -> PreparedStatement가 해제됨

```java
public void updateTurn(Team turn, int id) {
    String sql = "update board set turn = ? where id = ?";
    try (PreparedStatement preparedStatement = connection.prepareStatement(
            sql)) {
        // preparedStatement 실행 로직 
    } catch (SQLException e) {
        e.printStackTrace();
    }
}
```