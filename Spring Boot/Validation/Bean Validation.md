#validation #groups 
Bean Validation은 Java 객체의 필드에 애노테이션을 선언함으로써 해당 필드가 준수해야 하는 규칙들을 정의할 수 있다. Spring Boot는 Bean Validation API를 지원하며, Hibernate Validator와 같은 구현체를 통해 쉽게 사용할 수 있다.
### Bean Validation의 주요 어노테이션

- `@NotNull`: 필드 값이 null이 아니어야 함을 지정
- `@Min`/`@Max`: 숫자 필드의 최소값과 최대값을 지정
- `@Size`: 문자열, 컬렉션, 배열 필드의 크기를 지정
- `@Email`: 문자열이 이메일 형식을 준수해야 함을 지정
---
```java
@Data
public class Item {

    private Long id;
    
    @NotBlank
    private String itemName;

	@NotNull
	@Range(min = 1000, max = 1000000)
    private Integer price;

	@NotNull
	@Max(9999)
    private Integer quantity;

    public Item() {
    }
	...
}

```
검증 로직을 모든 프로젝트에 적용할 수 있게 공통화하고 표준화 한 것이 Bean [[Validation]]이다. Bean Validation을 활용하면, 애노테이션 하나로 검증 로직을 편리하게 적용할 수 있다.

```java
package hello.itemservice.domain.item;  
  
import lombok.Data;  
import org.hibernate.validator.constraints.Range;  
  
import javax.validation.constraints.Max;  
import javax.validation.constraints.NotBlank;  
import javax.validation.constraints.NotNull;  
  
@Data  
public class Item {  
  
    private Long id;  
  
    @NotBlank  
    private String itemName;  
  
    @NotNull  
    @Range(min = 1000, max = 1000000)  
    private Integer price;  
  
    @NotNull  
    @Max(9999)  
    private Integer quantity;  
  
    public Item() {  
    }  
  
    public Item(String itemName, Integer price, Integer quantity) {  
        this.itemName = itemName;  
        this.price = price;  
        this.quantity = quantity;  
    }  
}
```
##### 검증 애노테이션
- `@NotBlank` : 빈값 + 공백만 있는 경우를 허용하지 않음.
	- `@NotBlank(message = "No Blank")`와 같이 메시지를 지정할 수 있음.
- `@NotNull` : `null`을 허용하지 않음.
- `@Range(min = 1000, max = 1000000)` : 범위 안의 값이어야 함.
- `@Max(9999)` : 최대 9999까지만 허용됨.

```java
public class BeanValidationTest {


    @Test
    void beanValidation() {
        ValidatorFactory factory = Validation.buildDefaultValidatorFactory();
        Validator validator = factory.getValidator();

        Item item = new Item();
        item.setItemName(" ");
        item.setPrice(0);
        item.setQuantity(10000);

        Set<ConstraintViolation<Item>> violations = validator.validate(item);
        for (ConstraintViolation<Item> violation : violations) {
            System.out.println("violation = " + violation);
            System.out.println("violation = " + violation.getMessage());
        }
    }
}
```
##### 검증기 생성
```java
ValidatorFactory factory = Validation.buildDefaultValidatorFactory();
Validator validator = factory.getValidator();
```
##### 검증 실행
```java
Set<ConstraintViolation<Item>> violations = validator.validate(item);
```
검증 대상 `item`을 직접 검증기에 넣고 그 결과를 받는다. `Set`에는 `ConstraintViolation`이라는 검증 오류가 담긴다.
따라서 결과가 비어있으면, 검증 오류가 없는 것이다.
##### 실행결과
```text
violation = ConstraintViolationImpl{interpolatedMessage='must be between 1000 and 1000000', propertyPath=price, rootBeanClass=class hello.itemservice.domain.item.Item, messageTemplate='{org.hibernate.validator.constraints.Range.message}'}
violation = must be between 1000 and 1000000

violation = ConstraintViolationImpl{interpolatedMessage='must not be blank', propertyPath=itemName, rootBeanClass=class hello.itemservice.domain.item.Item, messageTemplate='{javax.validation.constraints.NotBlank.message}'}
violation = must not be blank

violation = ConstraintViolationImpl{interpolatedMessage='must be less than or equal to 9999', propertyPath=quantity, rootBeanClass=class hello.itemservice.domain.item.Item, messageTemplate='{javax.validation.constraints.Max.message}'}
violation = must be less than or equal to 9999
```
---
`spring-boot-starter-validation` 라이브러리를 넣으면 자동으로 Bean Validator을 인지하고 스프링에 통합한다.
##### 스프링 부트는 자동으로 글로벌 Validator로 등록한다.
`LocalValidatorFactoryBean`을 글로벌 Validator로 등록한다. 이 Validator는 `@Notnull`과 같은 애노테이션을 보고 검증을 수행한다.
즉, 글로벌 Validator가 적용되어 있기 때문에, `@Valid`, `@Validated`만 적용하면 된다.
>검증 오류가 발생하면, `FieldError`, `ObjectError을` 생성하고, `BindingResult`에 결과를 담아준다.

### 검증 순서
1. `@ModelAttribute` 각 필드에 타입 변환 시도
	- 실패할 경우 `typeMismatch`로 `FieldError` 추가
2. Validator 적용

>##### 바인딩에 성공한 필드만 Bean Validation 적용
>BeanValidator는 바인딩에 실패한 빌드는 BeanValidation을 적용하지 않는다.

`@ModelAttribute` -> 각각의 필드 타입 변환 시도 -> 변환에 성공한 필드만 BeanValidation 적용
##### 예시
- `itemName`에 문자 "A" 입력 -> 타입 변환 성공 -> `itemName` 필드에 BeanValidation 적용
- `price`에 문자 "A" 입력 -> "A"를 숫자 타입으로 변환 시도, 실패 -> typeMismatch FieldError 추가 -> `price` 필드는 BeanValidation 적용하지 않음.
---
### Bean Validation의 한계
---
### Bean Validation - groups
동일한 모델 객체를 등록할 때와 수정할 때 다음의 2가지 방법을 사용할 수 있다.
- **BeanValidation의 groups 기능을 사용**
- **Item을 직접 사용하지 않고, ItemService, ItemUpdateForm 같은 폼 전송을 위한 별도의 모델 객체를 만들어서 사용**

##### BeanValidation groups 기능 사용
**저장용 groups 생성**
```java
package hello.itemservice.domain.item;  
  
public interface SaveCheck {  
}
```

**수정용 groups 생성**
```java
package hello.itemservice.domain.item;  
  
public interface UpdateCheck {  
}
```

**상품 추가 컨트롤러 수정**
```java
@PostMapping("/add")  
public String addItem2(@Validated(SaveCheck.class) @ModelAttribute Item item, BindingResult bindingResult, RedirectAttributes redirectAttributes) {  
	...
}
```

**상품 수정 컨트롤러 수정**
```java
@PostMapping("/{itemId}/edit")  
public String edit2(@PathVariable Long itemId, @Validated(UpdateCheck.class) @ModelAttribute Item item, BindingResult bindingResult) {
	...
}
```
groups 기능은 사용 시 복잡도가 증가하기 때문에 실제 잘 사용되지 않는다.
수정의 경우 등록과 수정은 완전히 다른 데이터가 넘어온다. 예를 들어 회원 가입시 다루는 데이터와 수정시 다루는 데이터의 범위에는 차이가 있으며, 검증 로직도 달라진다. 따라서 별도의 객체로 데이터를 전달받는 방식을 사용한다.

이 방식을 사용하여 데이터 전달을 위한 별도의 객체를 사용하고, 등록, 수정용 폼 객체를 나누면 등록, 수정이 완전히 분리되기 때문에 `groups`를 적용하는 일이 없다.


