가설: @Query를 이용하면 entity에 작성한 @Where는 무시될 것이다.  
👉 NO! @Query로 직접 sql을 작성하였다 하더라도 Where이 무시되거나 하지는 않는다.

해결 방법
- @Query의 nativeQuery 옵션 이용
- @Where이 없는 Entity 새로 생성
- @Where 대신 @Filter 사용
  - @Filter: @Where와 같은 방식으로 작동하지만 세션 수준에서 활성화 또는 비활성화할 수도 있고 매개변수화할 수도 있음

***
참고
- https://stackoverflow.com/questions/57471733/how-to-opt-out-of-a-where-filter-for-an-individual-jpql-query
- https://stackoverflow.com/questions/2311125/ignore-hibernate-where-annotation
