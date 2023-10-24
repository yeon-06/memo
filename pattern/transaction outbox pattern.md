# Transaction outbox pattern
왜 등장하였는가
- 분산 시스템에서 발생하는 이중 쓰기 작업 문제 해결하기 위해 등장
  - 이중 쓰기 작업 문제: DB에 데이터를 보관하고, 다른 시스템에 알리기 위해 메시지를 보내야할 때 작업 중 하나에 장애가 나면 데이터가 일치하지 않을 수 있음
  - DB 업데이트 후, 이벤트 알림을 보낼 때 두 작업은 데이터의 일관성과 안정성을 보장하기 위해 원자적으로 실행되어야 함

언제 사용할 수 있는가
- DB update로 인해 이벤트 알람을 보내는 event-driven 기반 애플리케이션 구축중
- 2개 이상 서비스가 포함된 작업에서 원자성 보장하고 싶을 때 
- event sourcing pattern을 구현하기 원할 때

Transaction outbox pattern - RDB에서 사용 예제
- 애플리케이션은 DB update하고 outbox 테이블에 메시지 저장
- 다른 애플리케이션은 outbox에서 데이터를 읽고, 해당 데이터를 사용해 작업 수행
  - 실패시 완료될 때까지 재시도 가능 (at-least once 메시지가 성공적으로 전송되었는지 확인 가능)

***
참고
- https://docs.aws.amazon.com/prescriptive-guidance/latest/cloud-design-patterns/transactional-outbox.html
