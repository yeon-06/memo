### @ComponentScan vs @EnableAutoConfiguration

> AOP 적용하려면 적용해야하는 @EnableAspectJAutoProxy 없이도 AOP가 적용되어서 원인을 찾아보게 되었다.

@ComponentScan은 @Coponent 어노테이션을 스캔한다.  
@Configuration를 설정한 클래스와 함께 활용해 Spring의 구성요소를 스캔할 위치를 지정할 수 있다.

@EnableAutoConfiguration은 자동 configuration을 활성화한다.  
classpath에 포함된 jar 파일들과 직접 정의한 bean들을 기반으로 bean을 생성 및 등록할 수 있다.  
예를 들어 spring-boot-starter-web을 classpath에 주입 받는다면 Tomcat과 Spring MVC를 자동으로 구성해준다.  
(다만 직접 정의한 configuration보다 우선 순위가 낮다.)