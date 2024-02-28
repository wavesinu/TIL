**Bean Validation을 적용하고, bindingResult에 등록된 검증 오류 코드**
```
Field error in object 'item' on field 'itemName': rejected value []; codes [NotBlank.item.itemName,NotBlank.itemName,NotBlank.java.lang.String,NotBlank];
```
오류 코드가 마치 `typeMismatch`처럼 애노테이션 이름(`@NotBlank`)으로 등록되는 것을 볼 수 있다.
`NotBlank` 오류 코드를 기반으로 `MessageCodesResolver`를 통해 다양한 메시지 코드가 순서대로 생성된다.
### 메시지 등록
[[Bean Validation]]이 기본으로 제공하는 오류메시지를 변경하는 방법은 다음과 같다.

`errors.properties`
```properties
...
#Bean Validation 추가  
NotBlank={0} 공백X  
Range={0}, {2} ~ {1} 허용  
Max={0}, 최대 {1}
...
```
- `{0}`은 필드명이고, `{1}`, `{2}`, ... 는 각 애노테이션 마다 다름.
### Bean Validation 메시지 찾는 순서
1. 생성된 메시지 코드 순서대로 messageSource에서 메시지 찾기
2. 애노테이션의 `message` 속성 사용 -> `@NotBlank(message = "공백! {0}")`
3. 라이브러리가 제공하는 기본 값 사용 -> 공백일 수 없습니다.
