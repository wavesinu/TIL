```java
@RestController  
public class HelloController {  
  
    @GetMapping("/hello-v1")  
    public String helloV1(HttpServletRequest request) {  
        String data = request.getParameter("data"); //문자 타입 조회  
        Integer intValue = Integer.valueOf(data);   //숫자 타입으로 변경  
        System.out.println("intValue = " + intValue);  
        return "ok";  
    }  
}
```

HTTP 요청 파라미터는 모두 문자로 처리되므로, 요청 파라미터를 자바에서 다른 타입으로 변환 후 사용하려면 다음과 같이 숫자 타입으로 변환하는 과정을 거쳐야 한다.
- `Integer intValue = Integer.valueOf(data);`

스프링 MVC가 제공하는 `@RequestParam`을 사용하면 간단하게 처리할 수 있다.
```java
@GetMapping("/hello-v2")
    public String helloV2(@RequestParam Integer data) {
        System.out.println("data = " + data);
        return "ok";
    }
```

>`@ModelAttribute`, `@PathVariable`에서도 해당 타입 변환을 확인할 수 있다.

### Spring의 타입 변환 적용 예시
- 스프링 MVC 요청 파라미터
	- `@ModelAttribute`, `@PathVariable`, `@RequestParam`
- `@Value`등으로 YML 정보를 읽는 경우
- XML에 넣은 스프링 빈 정보를 변환하는 경우
- 뷰를 렌더링 하는 경우

개발자가 새로운 타입을 만들어서 변환하고 싶은 경우엔, Converter Interface를 사용하면 된다.
