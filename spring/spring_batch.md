- Spring Batch는 JobBuilderFactory을 통해 Job을 생성할 수 있다.
- job은 여러 step으로 구성될 수 있다.
- step은 StepBuilderFactory을 통해 생성할 수 있다.

itemReader: 데이터 생성
itemProcessor: 데이터 처리
itemWriter: 데이터 출력
