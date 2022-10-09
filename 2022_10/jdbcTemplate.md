토비의 스프링 5장을 읽으며 Transactional Manager에 대해 간단하게 학습했다.
[Connection을 Service에서 수정하는 경험](https://github.com/yeon-06/toby-spring/pull/7#issue-1398736368)을 했는데 Service에서 Connection을 close한다는 것이 생소하게 느껴졌다.
여지껏 단순한 로직들만 작성해봐서 어떤 자원을 open하면 해당 오브젝트에서 전부 close을 해왔고 try-with-resources를 애용해왔다
궁금증에 JdbcTemplate은 이를 어떻게 구현했을까 코드를 까보기 되었다.

DataSourceUtils를 이용해 Connection을 어떻게 처리할지 결정하는 메서드가 있었다.
release(커넥션 유지) 또는 close(커넥견 종료)를 수행하는지에 대한 로직이 담겨있었고 Connection을 바로 종료할 필요는 없구나를 깨달았다

다만 자원이 닫히지 않고 열린 상태로 유지되면 성능상 좋지 않으니 close 처리를 어떻게 할지는 계속 고민해보아야 할 것 같다.
