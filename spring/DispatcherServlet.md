### DispatcherServlet의 역할
DispatcherServlet은 요청을 매핑하고 뷰를 처리하고, 예외를 핸들링하는 등 다양한 일을 한다. 이 일들을 처리하기 위해 special bean 이라는 친구들을 이용한다.
 
### Bean Type	Explanation
- HanlderMapping	요청을 처리할 핸들러와 인터셉터 목록을 가짐
- HandlerAdapter	DispatcherServlet이 요청에 매핑되는 Handler를 호출할 수 있도록 돕는 역할
- Handler가 실제로 호출되는 방식과 상관 없도록 도움
- HandlerExceptionResolver	예외 해결을 위한 전략
- ViewResolver	핸들러에서 반환된 String 기반의 View 이름을 실제로 응답에서 렌더링할 View로 전환
- LocaleResolver,
LocaleContextResolver	client가 사용중인 Locale과 time zone을 확인
- ThemeResolver	웹 애플리케이션에서 사용 가능한 theme 확인
- MultipartResolver	multi-part 요청을 parsing하기 위한 추상화
- FlashMapManager	redirect를 통해 한 요청에서 다른 요청으로 attribute를 전달할 때 사용하는 입출력 FlashMap을 저장하고 검색
 
Application은 request 처리를 위해 필요한 Special Bean Types를 정의할 수 있다. 각 Special Bean에 대해 WebApplicationContext를 확인하고 일치하는 타입이 없으면 DispatcherSerlvlet.properties에 나열된 기본 유형으로 대체된다.
