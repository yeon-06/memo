> 자세한 설명은 [블로그](https://yeonyeon.tistory.com/229) 를 참조해주세요

### @Aspect와 컴포넌트 스캔

컴포넌트 스캔은 @Component 어노테이션을 붙인 클래스 뿐 아니라 @Controller, @Service 등이 붙은 클래스도 컴포넌트 스캔 대상에 포함된다. 그런데 @Aspect 어노테이션도 컴포넌트 스캔의
대상이라고 설명한 곳이 많았다. 하지만 @Aspect가 붙은 클래스가 정상적으로 동작하려면 @Component 또는 @Bean 어노테이션을 이용해야 한다.

### @Aspect는 기본 스캔 대상이 아니다.

Spring의 빈 등록을 도와주는 ClassPathBeanDefinitionScanner 클래스의 주석을 살펴보자.

> The default filters include classes that are annotated with Spring's @Component, @Repository, @Service, or @Controller stereotype.
