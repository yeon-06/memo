기본
- Spring Batch는 JobBuilderFactory을 통해 Job을 생성할 수 있다.
- job은 여러 step으로 구성될 수 있다.
- step은 StepBuilderFactory을 통해 생성할 수 있다.

step 구성
- itemReader: 데이터 생성
  - bean으로 생성해야 jdbcTemplate이 잘 세팅된다. bean 등록하지 않으면 getJdbcTemplate()에서 NPE가 발생한다.
  - null을 return 하면 더이상 읽을 데이터가 없다고 판단한다.
  - DB 조회 결과를 항상 ""를 반환하는 현상이 발생된다면 값이 잘 매핑되었는지 확인하라. (단일 매핑이면 SingleColumnRowMapper를 사용하면 된다.)
- itemProcessor: 데이터 처리
- itemWriter: 데이터 출력
