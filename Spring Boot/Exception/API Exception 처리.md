스프링 부트에서 제공하는 기본 오류 방식을 통해 API 예외를 처리할 수 있다.
##### `BasicErrorController`
```java
@RequestMapping(produces = MediaType.TEXT_HTML_VALUE)
public ModelAndView errorHtml(
	HttpServletRequest request, HttpServletResponse response) {}

@RequestMapping
public ResponseEntity<Map<String, Object>> error(HttpServletRequest request) {}
```

- `errorHtml()` : `produces = MediaType.TEXT_HTML_VALUE` : 클라이언트 요청의 Accept 헤더 값이 `text/html`인 경우에는 `errorHtml()`을 호출해서 view를 제공한다.
- `error()` : 그외의 경우에 호출되고, `ResponseEntity`로 HTTP Body에 JSON 데이터를 반환한다.

>**스프링 부트의 예외 처리**
>- 스프링 부트의 기본 설정은 오류 발생 시 `/error`를 오류 페이지로 요청하며, `BasicErrorController`는 이 경로를 기본으로 받는다.
>- `server.error.path`로 수정이 가능함.