# update set에는 and를 쓰지 마세요

### 문제
```
update table set field1=1 and field2=2 where field3 > 3;
```
- 예상: field1, field2의 값이 변경된다.
- 실제: field1의 값이 0으로 변경된다.
- 원인: and가 나열이 아닌 조건으로 인식된다. (1이 true이고, field2 = 2가 true인지 두 개의 조건을 and로 검사)

### 해결
```
update table set field1=1, field2=2 where field3 > 3;
```
- 반드시 and가 아닌 ,로 만들자

### 추가 조언
- 운영에서 U, D쿼리는 반드시 백업 데이터를 만들고, pk로 조회하자
