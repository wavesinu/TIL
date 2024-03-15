스프링은 API 예외 처리 문제를 해결하기 위해 `@ExceptionHandler` 애노테이션을 제공한다.
- 이를 통해 개발자는 예외를 직접 처리할 수 있다.
- API의 응답 본문이나 HTTP 상태 코드를 직접 정의할 수 있다.

해당 애노테이션을 통해 예외를 처리하는 기능을 `ExceptionHandlerExceptionResolver`라고 한다.
# @ExceptionHandler 예외 처리 방법
`@ExceptionHandler` 애노테이션을 선언하고, 해당 컨트롤러에서 처리하려는 예외를 지정한다. 해당 컨트롤러에서 예외가 발생하면, 해당 메서드가 호출된다.
- **특정 예외 타입을 처리하는 메서드에 `@ExceptionHandler` 애노테이션을 선언**
```java
@Controller
public class MyController {

    @ExceptionHandler(value = Exception.class)
    public ResponseEntity<Object> handleException(Exception ex) {
        // 예외 처리 로직
        return new ResponseEntity<>("error", HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```
- **하나의 메서드로 여러 타입의 예외를 처리하려면, 애노테이션의 `value` 속성에 예외 클래스 배열을 전달**
```java
@ExceptionHandler({NullPointerException.class, IllegalArgumentException.class})
public ResponseEntity<Object> handleMultipleExceptions(Exception ex) {
    // 예외 처리 로직
}
```
