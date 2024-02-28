`@Valid`, `@Validated`는 `HttpMessageConverter(@RequestBody)`에도 적용할 수 있다.
>`@ModelAttribute`는 HTTP 요청 파라미터(URL 쿼리 스트링, POST Form)를 다룰 때 사용함.
>`@RequestBody`는 HTTP Body의 데이터를 객체로 변환할 때 사용함. 주로 API JSON 요청을 다룰 때 사용함.

```java
@Slf4j
@RestController
@RequestMapping("/validation/api/items")
public class ValidationItemApiController {

    @PostMapping("/add")
    public Object addItem(@RequestBody @Validated ItemSaveForm form, BindingResult bindingResult) {

        log.info("API 컨트롤러 호출");

        if (bindingResult.hasErrors()) {
            log.info("검증 오류 발생 errors={}", bindingResult);
            return bindingResult.getAllErrors();    //FieldError, ObjectError 모두 반환
        }

        log.info("성공 로직 실행");
        return form;
    }
}
```
##### API의 경우 3가지 경우를 나누어 생각해야 한다.
- **성공 요청** : 성공
- **실패 요청** : JSON을 객체로 생성하는 것 자체가 실패
- **검증 오류 요청** : JSON을 객체로 생성하는 것은 성공했고, 검증에서 실패
---
### @ModelAttribute vs @RequestBody
HTTP 요청 파라미터를 처리하는 `@ModelAttribute`는 각각의 필드 단위로 적용된다. 따라서 특정 필드에 타입이 맞지 않는 오류가 발생해도 나머지 필드는 정상 처리할 수 있다.

`HttpMessageConverter`는 `@ModelAttribute`와 다르게 각각의 필드 단위로 적용되는 것이 아니라, 전체 객체 단위로 적용된다. 따라서 메시지 컨버터의 작동이 성공해서 `Item` 객체를 만들어야 `@Valid`, `@Validated`가 적용된다.

이를 정리해보자면, 
- `@ModelAttribute` : 필드 단위로 정교하게 바인딩이 적용된다. 특정 필드가 바인딩 되지 않아도 나머지 필드는 정상적으로 바인딩 되고, Validator을 사용한 검증도 적용할 수 있다.
- `@RequestBody` : HttpMessageConverter 단계에서 JSON 데이터를 객체로 변경하지 못하면, 이후 단계가 진행되지 않고, 예외가 발생한다. **컨트롤러도 호출되지 않고 Validator도 적용할 수 없다**.
	
>HttpMessageConverter 단계에서 실패하면 예외가 발생한다. 예외 발생시 원하는 양식으로 예외를 처리할 수 있다.

