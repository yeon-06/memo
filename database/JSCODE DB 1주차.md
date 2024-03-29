### 파일시스템과 데이터베이스의 차이점에 대해서 설명해주세요.

- 파일시스템: 데이터를 파일에 저장, 관리하는 시스템
- DB: 효율적인 검색을 위해 상호 연결된 데이터 집합으로 DBMS를 통해 데이터 생성, 삭제 등의 다양하고 편리한 기능을 제공

(+) 왜 파일시스템이 아니고 데이터베이스를 사용해야하는가?
- 정말 작은 양의 데이터만 존재한다면 오히려 파일 시스템이 효율적일 수 있음. 데이터가 많아질수록 데이터를 관리하기 편한 것은 DB

### 데이터베이스의 특징에 대해 설명해주세요.

- 계속적 변화: 항상 최신 데이터로 유지
- 동시 공유: 여러 사용자와 함께 사용
- 실시간 접근: 질의에 대한 실시간 처리 및 응답
- 내용에 의한 참조: 데이터 내용에 의한 직접 참조 가능
- 데이터의 독립성


### DBMS는 뭘까요? 특징에 대해 설명해주세요.

- 데이터베이스 관리 시스템
- DB를 조작하는 프로그램. 사용자 요구에 따라 정보를 생성하고 DB를 관리하는 소프트웨어.


### 스키마가 뭘까요? 3단계 데이터베이스 구조에 대해 설명해주세요.

- : 데이터베이스 구조나 제약조건 등을 정의한 메타데이터
- 외부 스키마: 테이블 같이 응용 프로그램의 관점에서 보는 스키마
- 개념 스키마: ER같은 데이터의 논리적 구조와 관계
- 내부 스키마: DBMS, B-Tree 같은 데이터의 물리적인 저장구조


### 데이터 독립성에 대해서 설명해주세요.

- DB 구조와 데이터의 내용이 서로 영향을 미치지 않는 것
- 논리적 데이터 독립성
  - : 테이블 속성이나 관계가 추가되어도 기존의 쿼리나 트랜잭션은 그대로 유지되는등, 논리적 구조가 변경되어도 응용 프로그램이나 사용자에 영향 X
  - 개념 스키마나 외부 스키마가 변경되어도 서로 영향 X
- 물리적 데이터 독립성
  - : 파일 저장 방식이나 인덱스 구성이 바뀌어도 DB의 스키마나 데이터는 그대로 유지되는 등, 물리적 구조가 변경되어도 데이터의 내용에 영향 X
  - 내부 스키마나 개념 스키마가 변경되어도 서로 영향 X


### RDBMS(관계형 데이터베이스 관리시스템)는 뭘까요?

- 데이터 관계를 중심으로 구현한 데이터베이스
- 행과 열을 가진 테이블 구조로, 외래키 등의 개념을 이용해 테이블끼리 관계를 만들어낼 수 있음
- Oracle, MySQL 등

### 릴레이션 스키마와 릴레이션 인스턴스에 대해서 설명해주세요.

![image](https://github.com/yeon-06/memo/assets/53105735/78514e80-df67-4534-a5e7-da4858a7ecbf)

- 릴레이션 스키마: 릴레이션에 담길 정보가 어떤 정보일지 정의
- 릴레이션 인스턴스: 릴레이션 스키마에 저장된 데이터의 집합

### 릴레이션의 차수와 카니덜리티에 대해 설명해주세요.

- 차수 = 디그리 = 속성의 수
  - 속성: 테이블에서 이름을 갖는 하나의 열. 개체의 특징.
- 카디널리티: 튜플의 수

### 키(Key)에 대해서 설명해주세요. (슈퍼키, 후보키, 기본키, 대리키, 외래키)

> 튜플 = 행 = 속성의 모임
> 속성 = 열

- 슈퍼키: 튜플을 유일하게 식별할 수 있는 속성들의 집합
- 기본키: 튜플을 식별하기 위해 필요한 키. 중복되지 않고, null을 가질 수 없음
- 후보키: 기본키가 될 수 있는 후보들
- 대체키: 후보키 중, 기본키를 제외한 나머지
- 외부키: 다른 테이블의 기본키를 참조하는 속성

### 무결성 제약조건에 대해서 설명해주세요. (도메인 무결성, 개체 무결성, 참조 무결성)

- 도메인 무결성: 열의 값은 일관성을 가져아한다. 열의 값이 t/f같이 일정 범위로 제한한다던가, 값이 not null이라던가.
- 개체 무결성: 유일한 식별자에 대한 요구. 기본키는 중복이 없고 null이 불가하다.
- 참조 무결성: 기본키와 외래키의 관계가 항상 정확하게 유지되어야한다. 타테이블의 데이터가 수정되어도, 데이터간 참조관계를 정확히 유지.

### 사용했던 데이터베이스에 대해서 설명해주세요. (오라클DB, MySQL, MariaDB, MongoDB 등)
주로 MySQL를 사용했고 테스트 목적으로 H2를 사용한 경험도 있습니다.  
- H2
  - 인메모리 DB
    - 데이터를 휘발성 메모리에 저장
    - 인메모리가 아닌 DB는 데이터를 보통 디스크에 저장 -> 이 디스크 접근이 느리기 때문에 인메모리 DB의 성능이 빠르다고 알려짐
- MySQL
  - 관계형 데이터베이스
  - RDB에서는 MySQL과 Oracle이 유명한데 비용상 문제로 보통 MySQL 사용

---
출처
- 코딩팩토리
- IT위키
- 정보통신기술용어해설
- wiki
