### LocalDate / LocalTime / LocalDateTime

- 시간대 (ZoneOffSet, ZoneRegion)에 대한 정보 미포함
- LocalDate: 날짜에 대한 정보
- LocalTime: 시간에 대한 정보
- LocalDateTime: 날짜 및 시간에 대한 정보

### ZoneOffSet

- UTC 기준의 시간
- ex: 우리나라는 UTC +09:00으로 표기

### ZoneRegion

- 타임존
- ex: 우리나라는 Asia/Seoul 사용

> ❓ ZoneOffSet vs ZoneRegion  
언뜻 보기에는 UTC +09:00와 Asia/Seoul을 볼 때 차이가 없는 것처럼 느껴진다. 이 둘은 왜 분리하여 사용할까? 이 이유는 DST(Daylight saving time; 써머 타임) 같은 Time Transition Rule 포함 여부 때문이다. ZoneOffset은 Time Transition Rule을 미포함하고 ZoneRegion은 Rule이 포함될 수도 있다.

### OffsetDateTime

- LocalDateTime + ZoneOffset

### ZonedDateTime

- LocalDateTime + ZoneOffset + ZoneRegion
- 서머 타임과 같은 Time Transition Rule을 ZoneRules를 이용해 내부적으로 계산

### Instant

- unix timestamp를 구할 때 사용
- 어느 순간(시간)을 나타내는 클래스
