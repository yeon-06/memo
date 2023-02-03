# Java 명명 규칙
> [네이버 캠퍼스 핵데이 Java 코딩 컨벤션](https://naver.github.io/hackday-conventions-java/)

### 클래스
- 영문+숫자+언더스코어 구성
- 대문자 카멜케이스   
  (ex: camel_case X, camelCase X, CamelCase O)
- 명사형
- 테스트 클래스 이름은 *Test

### 변수
- 영문+숫자+언더스코어 구성
- 소문자 카멜케이스  
  (ex: camel_case X, camelCase O, CamelCase X)
- 임시 변수 외에는 1글자 이름 사용 X
- 상수는 대문자+언더스코어 구성
  (ex: MAX_NUMBER)

### 메소드
- 영문+숫자+언더스코어 구성
- 소문자 카멜케이스  
  (ex: camel_case X, camelCase O, CamelCase X)
- 동사/전치사로 시작

### 패키지
- 소문자로 구성

### 인터페이스
- 대문자 카멜케이스  
  (ex: camel_case X, camelCase X, CamelCase O)
- 명사, 형용사 이용

### 공통
- 한국어 발음대로 표기 금지  
  (ex: 사용자 -> Sayongja X, User O)
- 대문자로 표기할 약어는 목록에 별도로 명시
  (ex: 대문자로 표기할 약어의 목록을 정의하지 않는 경우 : HttpApiUrl  
       API만 대문자로 표기할 약어의 목록에 있을 경우 : HttpAPIUrl  
       HTTP, API, URL이 대문자로 표기할 약어의 목록에 있을 경우 : HTTPAPIURL )  

***
명명 규칙 이외의 팁
- import의 경우 * 사용하지 않기 (static import일때는 허용)
- 제한자 순서: public -> protected -> private -> abstract -> static -> final -> transient -> volatile -> synchronized -> native -> strictfp
- long형 마지막에는 L (ex: long base = 123L;)