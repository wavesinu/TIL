# @ModelAttribute의 특별한 사용법
```java
    @ModelAttribute("regions")
    public Map<String, String> regions() {
        Map<String, String> regions = new LinkedHashMap<>();
        regions.put("SEOUL", "서울");
        regions.put("BUSAN", "부산");
        regions.put("JEJU", "제주");
        return regions;
		// model.addAttribute("regions", regions); 가 자동으로 들어감 
    }

```
`@ModelAttribute`는 컨트롤러에 있는 별도의 메서드에 적용할 수 있다. 이렇게 하면 해당 컨트롤러를 요청할 때 `regions`에서 반환한 값이 자동으로 모델(`model`)에 담기게 된다.
물론 이렇게 사용하지 않고, 각각의 컨트롤러 메서드에서 모델에 직접 데이터를 담아서 처리해도 된다.
