- jdk 1.0
- jdk 1.1
    - Java Beans
    - Inner Class
    - Reflection
    - RMI
    - 유니코드 지원
- jdk 1.2
    - Swing이 SE에 포함
    - Coarba IDL: 이종기기간 함수 호출 스펙
    - Collection Framework
- jdk 1.3
    - HotSpot: Sun에서 만든 JIT 구현
    - JNDI: 디렉토리 및 이름으로 원하는 서비스 찾기
- jdk 1.4
    - 정규표현식
    - assert
    - Non-Blocking IO
    - XML API
    - Java Web Start
- jdk 1.5
    - Generics
    - Annotation
    - Auto Boxing/Unboxing
    - Enumeration
    - 가변 길이 파라미터
    - static import
    - java.util.Scanner
- java 6
    - GC 지원
- java 7
    - Diamond Operator <>
    - switch문에서 String 사용
    - Dynamic Language 지원
- java 8
    - Lambda
    - Oracle JDK, OpenJDK 2가지로 나뉨
    - new Date and Time API
    - Stream
    - Optional
- java 9
    - jigsaw 기반으로 런타임이 모듈화됨
- java 10
    - var 키워드
    - 병렬 처리 GC 도입 -> 성능 향상
    - 개별 스레드로 분리된 stop-the-world
    - java 기반 JIT 컴파일러 추가
- java 11
    - Oracle JDK, OpenJDK 통합
    - 유료화로 인해 서드파티 JDK로 이전 필요
- java 12
    - switch문 확장
- java 13
    - switch문 개선을 위한 yield 예약어 추가
- java 14
    - instanceof 패턴 매칭
    - record라는 데이터 오브젝트 선언 추가
- java 15
    - EdDSA 암호화 알고리즘 추가
    - 스케일링 가능한 낮은 지연의 가비지 컬렉터 추가
    - 외부 메모리 접근 API
    - 상속 가능한 클래스를 지정할 수 있는 봉인 클래스 제공
- java 16
    - Vector API
    - 유닉스 도메인 소켓 지원
    - jpackage 명령어: OS별 자바 프로그램 설치 패키지로 생성하는 기능
- java 17
    - 의사난수 생성기를 통한 예측이 어려운 난수 생성 API
    - 봉인 클래스 정식 추가
    - 컨텍스트 기반의 역직렬화 필터링

<br>


❓ **annotation**이란?

👉 인터페이스를 기반으로 한 문법으로 클래스나 메소드 등에 특별한 의미를 부여하기 위해 사용

<br>


❓ **Reflection**이란?

👉 객체를 통해 클래스의 정보를 분석하는 프로그램 기법

👉 Spring은 런타임 시 개발자가 등록한 bean을 애플리케이션에서 가져와 사용할 수 있게 됨

😢 Reflection을 사용하지 않은 코드에 비해 성능 ↓

<br>


❓ **Java 7 → Java 8 변화의 이유**

👉 Stream, Lambda: 함수형 프로그래밍의 도입

👉 Time: Date는 불변 객체가 아니기 때문에 새롭게 LocalDate 등장


<br>


❓ **Stream API**란?

👉 데이터 추상화하고 자주 사용되는 함수들을 정의한 API

- 원본의 데이터 변경 X
- 일회용

<br>


❓ **Lambda**란?

👉 함수를 하나의 식으로 표현한 것

- 메소드의 이름이 필요 없어 익명 함수의 한 종류라 취급
- 일급 객체

<br>


❓ **함수형 프로그래밍; FP**

👉 프로그래밍을 순수 함수로 나누어 문제를 해결하는 기법. 작은 문제를 해결하기 위한 함수를 작성해 가독성 높이고 유지보수 용이하게 함
