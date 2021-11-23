> 간략적인 내용만 담았고 더 디테일한 설명은 블로그에 정리해두었다.
> https://yeonyeon.tistory.com/163

## DTO; Data Transfer Object
- 계층간 데이터 교환을 위한 객체
- 로직을 가지지 않은 getter/setter 메소드만 갖는 객체
- request와 response용 DTO는 view를 위한 클래스
 

## VO; Value Object
- 특정 비즈니스 값을 담는 객체
- DTO와 유사하나 read only 속성을 가짐
- 모든 속성 값이 같다면 같은 객체임을 의미  
  (ex: 지폐에는 각 고유번호가 존재한다. 하지만 우리는 만원짜리 두 장을 보면 만원이 2장 있다고 인식하지 고유번호 A인 지폐 하나, 고유번호 B인 지폐 하나로 인식하지 않는다.)
- 생성자 외에 setter 속성을 띄는 메소드 선언 금지
 
 
## Entity
- 실제 DB 테이블과 매칭되는 클래스
- 외부에서 getter 메소드를 이용하지 않도록 필요한 로직 구현
- DB 테이블 내에 존재하는 컬럼만을 속성으로 가지는 클래스
- request, response 클래스로 사용 X

## 요약
1. DTO: 계층간 데이터 전송
2. VO: 의미있는 값 표현할 때 사용
3. Entity: DB 테이블과 매핑되는 클래스
  
||DTO|VO|Entity|
|---|---|---|---|
|값 변경|O|X|O|
|로직 포함|X|O|O|

