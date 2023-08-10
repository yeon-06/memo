### group by는 집계함수(aggregation function)과 함께 사용해야 한다.

> 집계 함수 = sum(), min(), max(), ...

상황
- 상품에는 id, price 필드가 있다.
- max()가 아닌 order by와 limit으로 id별 price 최대값을 알 수 있지 않을까?

문제 발생 원인
- group by는 집계함수를 통해 시스템에게 필드의 결합 방식을 알릴 수 있다

***
참고
- https://stackoverflow.com/questions/20074562/group-by-without-aggregate-function
- https://www.w3schools.com/sql/sql_groupby.asp
