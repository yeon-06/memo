
===
객체지향 쿼리 언어1 - 기본문법
JPQL
QueryDSL
네이티브SQL 등등 다양한 쿼리 방법을 지원하는 JPA

JPQL
- 가장 단순한 조회 방법: find()
- 객체 그래ㅍ 탐색 a.getB()
- DB에서 필요한 데이터만 불러올 때 검색조건 포함된 SQL 필요!
- SQL 문법과 유사
-

Criteria 복잡해서 실무에서는 잘 사용 x하기도 함
QueryDSL 권장

queryDSL
세팅은 좀 힘들 수 있지만 사용하기 정말 편함
JPQL을 알고 QueryDSL을 사용해야 함

JPQL 문법
- 엔티티와 속성 대소문자 구분
- select, from 같은 키워드는 대소문가 구분 x
- 테이블 이름이 아닌 엔티티 이름 사용 (별도 지정한게 없으면 클래스명과 동일)
- 별칭 필수
