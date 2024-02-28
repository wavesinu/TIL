### 타임리프에서 ENUM 직접 사용하기
```java
@ModelAttribute("itemTypes")  
public ItemType[] itemTypes(){  
    return ItemType.values();  
}
```
- 모델에 ENUM을 담아서 전달하는 대신에 타임리프는 자바 객체에 직접 접근할 수 있다.
### 타임리프에서 ENUM 직접 접근
```HTML
<div th:each="type : ${T(hello.itemservice.domain.item.ItemType).values()}">
```
- 스프링EL 문법으로 ENUM을 직접 사용할 수 있다. ENUM에 `values()`를 호출하면 해당 ENUM의 정보가 배열로 반환된다.
그러나 이렇게 사용하면 ENUM의 패키지 위치가 변경될 때 자바 컴파일러가 타임리프까지 컴파일 오류를 잡을 수 없으므로, 추천되지 않는다.