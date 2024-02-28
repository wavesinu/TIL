스프링은 검증을 체계적으로 제공하기 위해 다음 인터페이스를 제공한다.
```java
public interface Validator {
	boolean supports(Class<?> clazz);
	void validate(Object target, Errors errors);
}
```
