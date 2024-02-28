애플리케이션의 여러 로직에서 공통으로 관심있는 것을 **공통 관심사(cross-cutting concern)**라고 한다.
공통 관심사는 스프링의 AOP로 해결할 수 있지만, 웹과 관련된 공통 관심사는 서블릿 필터나 스프링 인터셉터를 사용하는 것이 좋다.
웹과 관련된 공통 관심사를 처리할 때는 HTTP의 헤더나 URL의 정보들이 필요한데, 서블릿 필터나 스프링 인터셉터는 `HttpServletRequest`를 제공한다.

# 서블릿 필터 소개
필터는 서블릿이 지원하는 수문장이다. 필터의 특성은 다음과 같다.
##### 필터 흐름
```
HTTP 요청 -> WAS -> 필터 -> 서블릿 -> 컨트롤러
```
- 필터를 적용하면 필터가 호출된 다음에 서블릿이 호출된다.
	- 고객의 요청 로그를 남기는 요구사항이 있는 경우, 필터를 사용하면 됨.
	- 필터는 특정 URL 패턴에 적용할 수 있다. (`/*` : 모든 요청에 필터가 적용된다.)
##### 필터 제한
```
HTTP 요청 -> WAS -> 서블릿 -> 컨트롤러 // 로그인 사용자
HTTP 요청 -> WAS -> 필터  (적절하지 않은 요청이라 판단, 서블릿 호출 X)// 비 로그인 사용자
```
##### 필터 체인
```
HTTP 요청 -> WAS -> 필터1 -> 필터2 -> 필터3 -> 서블릿 -> 컨트롤러
```
- 필터는 체인으로 구성되는데, 중간에 필터를 자유롭게 추가할 수 있다.
	- 예를 들어서 로그를 남기는 필터를 먼저 적용하고, 그 다음 로그인 여부를 체크하는 필터를 만들 수 있음.
##### 필터 인터페이스
```java
package javax.servlet;

import java.io.IOException;

public interface Filter {
    default void init(FilterConfig filterConfig) throws ServletException {
    }

    void doFilter(ServletRequest var1, ServletResponse var2, FilterChain var3)
    throws IOException, ServletException;

    default void destroy() {
    }
}
```
>필터 인터페이스를 구현하고 등록하면, 서블릿 컨테이너가 필터를 싱글톤 객체고 생성하고 관리한다.

- `init()` : 필터 초기화 메서드, 서블릿 컨테이너가 생성될 때 호출됨.
- `doFilter()` : 고객의 요청이 올 때마다 해당 메서드가 호출됨. 필터의 로직을 구현하는 부분
- `destroy()` : 필터 종료 메서드, 서블릿 컨테이너가 종료될 때 호출됨.
---
# Servlet 필터 - 인증 체크