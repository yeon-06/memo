# NoClassDefFoundError 에러

ClassNotFound와 비슷해보이지만 조금 다르다.
일반적으로 컴파일 시점에는 존재했으나 런타임에 존재하지 않으면 발생한다.
jar파일로 묶었을 때 외부 라이브러리가 빠진 경우 해당 클래스를 호출하는 경우에 생겼다.
해결 방법은 해당 라이브러리가 정상적으로 포함되어 jar로 묶이도록 하면 된다.