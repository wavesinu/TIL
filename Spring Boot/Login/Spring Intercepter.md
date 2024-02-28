스프링 인터셉터도 [[Servlet 필터]]와 같이 웹과 관련된 공통 관심 사항을 효과적으로 해결할 수 있는 기술이다.
스프링 인터셉터는 스프링 MVC가 제공하는 기술이며, 둘 다 웹과 관련된 공통 관심 사항을 처리하지만, 적용되는 순서와 범위, 그리고 사용방법에서 차이가 있다.
##### 스프링 인터셉터 흐름
```
HTTP 요청 -> WAS -> 필터 -> 서블릿 -> 스프링 인터셉터 -> 컨트롤러
```
- 스프링 인터셉터는 디스패처 서블릿과 컨트롤러 사이에서 컨트로러 호출 직전에 호출된다.
- 스프링 인터셉터는 [[스프링 MVC]]가 제공하는 기능이므로, 결국 디스패처 서블릿 이후에 등장한다.
	- 스프링 MVC의 시작점이 디스패처 서블릿이라고 생각하면 됨.
- 스프링 인터셉터에도 URL 패턴을 적용할 수 있는데, 서블릿 URL 패턴과 다르고, 정밀하게 설정할 수 있다.
##### 스프링 인터셉터 제한
```
HTTP 요청 -> WAS -> 필터 -> 서블릿 -> 스프링 인터셉터 -> 컨트롤러 //로그인 사용자
HTTP 요청 -> WAS -> 필터 -> 서블릿 -> 스프링 인터셉터 //비 로그인 사용자
```
##### 스프링 인터셉터 체인
```
HTTP 요청 -> WAS -> 필터 -> 서블릿 -> 인터셉터1 -> 인터셉터2 -> 컨트롤러
```
### 스프링 인터셉터 인터페이스
```java
package org.springframework.web.servlet;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import org.springframework.lang.Nullable;

public interface HandlerInterceptor {
    default boolean preHandle(HttpServletRequest request,
	    HttpServletResponse response,
		Object handler) throws Exception {
        return true;
    }

    default void postHandle(HttpServletRequest request,
	    HttpServletResponse response,
		Object handler,
		Nullable ModelAndView modelAndView) throws Exception {
    }

    default void afterCompletion(HttpServletRequest request,
	    HttpServletResponse response,
	    Object handler, 
	    @Nullable Exception ex) throws Exception {
    }
}
```
- 인터셉터는 컨트롤러 호출 전(`preHandle`), 호출 후(`postHandle`), 요청 완료 이후(`afterCompletion`)와 같이 단계적으로 세분화 되어 있다.
- 인터셉터는 어떤 컨트롤러가 호출되는지에 대한 호출 정보를 받을 수 있다.
	- + 어떤 `modelAndView`가 반환되는지 응답 정보도 받을 수 있다.