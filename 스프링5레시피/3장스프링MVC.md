# 스프링 MVC
###### MVC 패턴의 핵심은 UI와 비즈니스 로직을 분리해서 서로 영향을 미치지 않고 독립적으로 수정할 수 있게 한다는 사상이다.

## 스프링 MVC 구동
`@Controller` 를 붙인 클래스에 요청이 들어오면 스프링은 적합한 핸들러 메서드를 찾는다. 
`@RequestMApping` 을 붙이면 핸들러 메서드로 임명된다. 핸들러 메서드는 요청 처리후 제어권을 뷰에게 넘긴다.
##### 뷰리졸버(ViewResolver 인터페이스 구현)를 이용해 논리뷰 이름(user.jsp or report.pdf)을 실제뷰 구현체(HTML, JSP, PDF)로 해석

#### Servlet 설정
`ServletContainerInitializer` 필수 서블릿을 정의 여러개도 가능하다. 스프링이 감지할려면
`META-INF/services` 디렉토리에 `javax.servlet.ServletContainerInitializer` 파일을 만들고 ex)`com.apress.springrecipes.court.web.CourtServletContainerInitializer` 추가한다.

다른 방법으로 `SpringServletContainerInitializer` 사용하면 애는 클래스 패스에서 `WebApplicationInitiallizer` 인터페이스 구현테를 찾는다. `AbstractAnnotationConfigDispatcherServletInitializer` 고 그중하나임 요인터페이스로 구현해주면 동일하게 작동함


#### ViewResolver 설정
`InternalResourceViewResolver` 빈을 구성 노리뷰 이름을 jsp파일로 해석


#### 인터셉터 
 
- `HandlerIntercepter` 인터페이스 구현
- 콜백메서드 구현 : `preHandle()` 메소드핸들러 시작전,`postHandle()` 메소드햔들러 직후,`afterCompletion()` 요청처리가 끝난(뷰 렌더링까지 완료)
- `HandlerInterceptorAdapter` 인터페이스 구현해도됨
- `WebMvcConfigurer` 인터페이스를 구현한 class에 `addInterceptors()` 오버라이드해 추가
- `addPathPattern()`, `excludePathPatterns()` url 지정 가능 