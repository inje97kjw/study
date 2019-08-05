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

### 유저로케일
- `LocaleResolver` 인터페이스를 구현한 로케일 리졸버가 식별함
- `DispatcherServlet`가 감지할려면 빈 명을 `localeResolver`이라고 명명  `DispatcherServlet`당 하나만 등록 가능하다.
- 세션으로 : `SessionLocaleResolver` accept-language 헤더로 기본로케일 결정, default 설정가능
- 쿠키로 : `CookieLocaleResolver` accept-language 헤더로 기본로케일 결정, default 설정가능
- 로케일변경 : 명시적으로 변경 가능하지만 `LocaleResolver.setLocale()` `LocaleChangeInterceptor` 핸들러 매핑에 적용 

### 로케일별 메세지
- `messageSource` 빈네임으로 명명
- `ResourceBundleMessageSource` 구현테를 등록하면 basename이 message인 리소스 번들을 로드
- message.properties,message_de.properties `de` 로케일 

### 뷰
- 뷰리졸버가 여러개인 경우 우선순위 `setOrder()` 를 지정해준다.

###  ContentNeotiationViewResolver

- 요청별로에 확장자가 있고 기본메디아 타입은 매치 되는 확장가가 없으면 HTTP Accept 해더를 활용

### 뷰에 예외 매핑

- `HandlerExceptionResolver` 에 `SimplemappingExceptionResolver` 에 exception의 종료와 매핑핳ㄹ view 네임을 설정할수 있다.
- `@ControllerAdvice` `@ExceptionHandler` 에 exception 을 지정할수 있다.


 
