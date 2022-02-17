> 패키지에 대한건 [패키지, 임포트, 클래스, 인스턴스 글](./Java_built_in_package.md)을 참고하길 바란다.  
> 전체 글: https://yeonyeon.tistory.com/191

패키지는 크게 Built-in packages와 User-defined packages로 나뉜다.

- `Built-in packages`: Java에서 우리 이미가 갖고 있는 다양한 선행 패키지들
- `User-defined packages`: 사용자가 정의한 패키지

### Built-in packages

- JDK나 JRD에 내장되어 제공하는 패키지
- JAR 파일 형식으로 제공됨
- 압축 해제 시 lang, io, util, SQL 등의 패키지가 포함된 것을 확인 가능

Oracle docs에서 JDK에 포함되는 모든 패키지들을 확인할 수 있다.

### 그렇다면 언제 어떤 메모리에 적재되는 것일까?

Runtime Data Area은 데이터가 저장되는 영역이다.  
크게 `Heap`, `Stack`, `Static`영역이 포함되어 있다 정도만 기억해두자.

이제 프로그램의 실행 과정을 살펴보자.

1. JRE(Java Runtime Environment)가 자바 프로그램 실행 시 `main()` 찾기
2. `main()` 존재 시, Class Loader가 목적 파일`.class` 실행
3. `static 영역`에 java.lang 패키지, import한 패키지들 적재
4. `stack 영역`에 `main()`의 호출 정보(stack frame) 적재
5. 변수 영역에 각 인자들 위치
6. `main()` 실행
7. `main()`의 `}`를 만나면 JRE가 JVM을 종료시켜 모든 메모리 제거

여기서 3을 주목하자!  
`java.lang`같은 빌트인 패키지는 3에서 import 패키지들과 함께 적재가 된다.
