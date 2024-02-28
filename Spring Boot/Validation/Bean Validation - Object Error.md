[[Bean Validation]]에서 특정 필드(`FieldError`)가 아닌 해당 오브젝트 관련 오류(`ObjectError`)는 `@ScriptAssert()`를 사용해서 처리할 수 있다.
```java
@Data
@ScriptAssert(lang = "javascript", script = "_this.price * _this.quantity >= 10000")
public class Item {
	...
}
```
그러나 실제 사용하는 경우에 제약이 많고 복잡하다. 또한 검증 기능이 해당 객체의 범위를 넘어서는 경우가 생길 때, 대응이 어렵다.
따라서 `ObjectError`(글로벌 오류)의 경우 오브젝트 오류 관련 부분만 직접 자바 코드로 작성하는 것이 권장된다.

##### ValidationItemControllerV3 - 글로벌 오류 추가
```java
@PostMapping("/add")
    public String addItem(@Validated @ModelAttribute Item item, BindingResult bindingResult, RedirectAttributes redirectAttributes) {

        //특정 필드가 아닌 복합 룰 검증
        // 자바 코드로 글로벌 오류 처리
        if (item.getPrice() != null && item.getQuantity() != null) {
            int resultPrice = item.getPrice() * item.getQuantity();
            if (resultPrice < 10000) {
                bindingResult.reject("totalPriceMin", new Object[]{10000, resultPrice}, null);
            }
        }
        
        //검증에 실패하면 다시 입력 폼으로 redirect
        if (bindingResult.hasErrors()) {
            log.info("errors ={} ", bindingResult); //bindingResult는 자동으로 view에 넘어감
            return "validation/v3/addForm";
        }
        //성공 로직
        Item savedItem = itemRepository.save(item);
        redirectAttributes.addAttribute("itemId", savedItem.getId());
        redirectAttributes.addAttribute("status", true);
        return "redirect:/validation/v3/items/{itemId}";
    }
```
