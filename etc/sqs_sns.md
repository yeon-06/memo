# SNS

- pub/sub 기반의 메시징 서비스
- 하나의 토픽을 여러 주체가 구독 (하나의 메시지를 여러 서비스에서 처리)
- 토픽에 전달된 내용을 구독한 모든 주체가 전달받아 처리 
- 전달 방식이 push (서비스에서 SNS로 push)

# SQS

- 다른 서비스에서 사용할 수 있도록 메시지를 잠시 저장하는 용도
- AWS 서비스들 간의 느슨한 연결을 수립하려 사용
- 하나의 메시지를 한번만 처리
- 전달 방식이 pull (서비스가 SQS로부터 pull)

*
- SNS-SQS 구독: https://docs.aws.amazon.com/ko_kr/sns/latest/dg/subscribe-sqs-queue-to-sns-topic.html 
