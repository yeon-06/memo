# group by 개선 방법

### 1. group by 건 필드에 인덱스 추가

- group by 필드에 인덱스 걸기 전 (where절에 index 걸려있어서 Using where이 뜨고있다)
```
Using index condition; Using where
```

- group by 필드에 인덱스 건 후
```
Using index condition; Using where; Using temporary; Using filesort
```

- https://jojoldu.tistory.com/476 

### 2. order by null
> 검증 필요

- count를 하는 경우 정렬이 불필요한데 group by로 인해 정렬 과정이 거쳐진다
- order by null를 통해 정렬 과정을 스킵할 수 있다
- http://www.mysqlkorea.com/sub.html?mcode=manual&scode=01&m_no=21460&cat1=7&cat2=217&cat3=238&lang=k 
