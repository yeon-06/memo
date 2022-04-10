> 우테코 - 네오의 강의를 듣고 정리한 글  
> subject: 자바 package, import, class, instance

## 정리 노트 😉

### package; 패키지

- 관련된 클래스들을 모아 관리
- 수백, 수천 개의 클래스를 찾을 수고를 덞
- 각 프로젝트나 소프트웨어 간의 소스 충돌 방지

#### package convention

- 일반적으로 회사 도메인명을 사용
- 소문자 사용
- java 또는 javax로 시작하는 이름 X (JDK에서 독점적으로 사용)

#### 패키지 vs 디렉토리

- 패키지: Java에서 경로를 나타냄
- 디렉토리: OS에서 경로를 나타냄

<br/>

### import; 임포트

- 모든 클래스 앞에 패키지명을 기입하지 않기 위해

> 클래스 앞에 패키지명을 기입하는 것을 **FQCN**(Fully Qualified Class Name)이라고 한다.

#### ❓ String, Integer는 import 안해도 new 생성 가능

👉 자바는 자주 사용하는 클래스를 `java.lang`에서 자동으로 import (빌트인 패키지)  
➕ sout에서 `System`도 클래스인데 `java.lang.System`에 존재하기 때문에 자동으로 import됨

> `Built-in Package`; `빌트인패키지`
> : 자바가 기본적으로 제공하는 패키지 및 클래스

#### ❓ jdk 구버전에서는 기본 경로에 있는건 import 하지 않아도 사용 가능

👉 사실임. 현재는 빌트인 패키지의 클래스와 혼동되고 명시적으로 보여주기 위해 개선됨

#### 클래스명이 같은 경우 import는 어떻게 될까?

👉 여러개 중 하나를 선택해야 한다. 하지만 이런 경우는 좋은 케이스가 아니니 클래스 명을 적절하게 변경하는 것을 추천.

<br/>

### class; 클래스

- 인스턴스를 생성하기 위한 template
- `클래스 메소드`: 인스턴스 생성하지 않아도 호출 가능 (=`유틸리티 메소드`)
- `클래스 필드`: 여러 인스턴스에서 공유하는 정보가 있는 경우 사용

#### ❓ 클래스 메소드로 만드는 방법

👉 `static` 키워드 사용

<br/>

### 인스턴스 (객체)

- 클래스를 통해 실체화되어 생성
- 상태를 갖고 메소드를 통해 변경될 수 있음
- `인스턴스 메소드`: 인스턴스의 상태 변경 또는 반환. 인스턴스 생성 후 호출 가능
- `인스턴스 필드`: 인스턴스의 상태 정보를 갖고 있는 변수 (=`상태 변수`)

#### ❓ 인스턴스 생성 막는 방법

👉 생성자를 private로 만들면 됨. (유틸에서 종종 사용)  
객체 생성을 허용해도 상관 없지만 모든 메소드가 클래스 메소드인 경우 인스턴스 생성을 명시적으로 막아주는 것이 보기 편함

## 과제 노트 🤩
- 이펙티브 자바 - 객체 생성과 파괴
- 정적 팩토리 메소드