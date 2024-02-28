HTML checkbox는 선택이 안 되면 클라이언트에서 서버로 값 자체를 보내지 않는다. 수정의 경우에는 상황에 따라 이 방식이 문제가 될 수 있다.
사용자가 의도적으로 체크되어 있던 값의 체크를 해제해도, 저장시 아무 값도 넘어가지 않기 때문에, 서버 구현에 따라서 값이 오지 않는 것으로 판단해서 값을 변경하지 않을 수도 있다.

이런 문제를 해결하기 위해 스프링 MVC는 히든 필드를 하나 만들어서 `_open`처럼 기존 체크 박스

```
itemName=123&price=23&quantity=2323&_open=on]
```
![[CleanShot 2024-01-28 at 13.26.35@2x.png]]
##### 체크 해제를 인식하기 위한 히든 필드
```HTML
<input type="hidden" name="_open" th:value="on"/>
```
##### 기존 코드에 히든 필드 추가
```HTML
<!-- single checkbox -->
        <div>판매 여부</div>
        <div>
            <div class="form-check">
                <input type="checkbox" id="open" name="open" class="form-check-input">
                <input type="hidden" name="_open" th:value="on"/>   <!--히든 필드 추가-->
                <label for="open" class="form-check-label">판매 오픈</label>
            </div>
        </div>
```
##### 실행 로그
![[CleanShot 2024-01-28 at 13.29.58@2x.png]]
##### 체크 박스 체크
`open=on&_open=on`
체크 박스를 체크하면 스프링 MVC가 `open`에 값이 있는 것을 확인하고 사용한다. 이때 `_open`은 무시한다.
##### 체크 박스 미크
`_open=on`
체크 박스를 체크하지 않으면 스프링 MVC가 `_open`만 있는 것을 확인하고 `open`의 값이 체크되지 않았다고 인식한다.
이 경우 서버에서 `Boolean` 타입을 찍어보면, 결과가 `null`이 아니라 `false`인 것을 확인할 수 있다.
`log.info("item.open={}", item.getOpen());`

---
# 타임리프에서 체크 박스
```HTML
<div>판매 여부</div>  
<div>  
    <div class="form-check">  
        <input type="checkbox" id="open" th:field="${item.open}" class="form-check-input">  
        <label for="open" class="form-check-label">판매 오픈</label>  
    </div>
</div>
```
또는
```HTML
<div>판매 여부</div>  
<div>  
    <div class="form-check">  
        <input type="checkbox" id="open" th:field="*{open}" class="form-check-input">  
        <label for="open" class="form-check-label">판매 오픈</label>  
    </div></div>
```
로 작성할 수 있다.

- `<input type="hidden" name="_open" value="on"/>`
타임리프를 사용하면 체크 박스의 히든 필드와 관련된 부분도 함께 해결해준다. HTML 생성 결과를 보면 히든 필드 부분이 자동으로 생성되어 있다.

**HTML 생성 결과**
```HTML
<hr class="my-4">
    <!-- single checkbox -->
    <div>판매 여부</div>
    <div>
        <div class="form-check">
            <input type="checkbox" id="open" class="form-check-input" disabled name="open" value="true">
            <label for="open" class="form-check-label">판매 오픈</label>
        </div>
    </div>
```
##### 타임리프의 체크 확인
체크 박스에서 판매 여부를 선택해서 저장하면, 조회 시에 `checked` 속성이 추가된 것을 확인할 수 있다.
타임리프의 `th:field`를 사용하면, 값이 `true`인 경우 체크를 자동으로 처리해준다.
---
# 멀티 체크박스
```java
<div>  
    <div>등록 지역</div>  
	    <div th:each="region : ${regions}" class="form-check form-check-inline">  
	    <input type="checkbox" th:field="*{regions}" th:value="${region.key}" class="form-check-input">  
        <label th:for="${#ids.prev('regions')}"  
               th:text="${region.value}" class="form-check-label">서울</label>  
  
    </div>
</div>
```

`th:for="${#ids.prev('regions')}"`
멀티 체크박스는 같은 이름의 여러 체크박스를 만들 수 있다. 그런데 문제는 이렇게 반복해서 HTML 태그를 생성할 때, 생성된 HTML 태그 속성에서 `name`은 같아도 되지만, `id`는 모두 달라야 한다. 따라서 타임리프는 체크박스를 `each` 루프 안에서 반복해서 만들 때 임의로 `1, 2, 3`과 같이 숫자를 뒤에 붙여준다.

![[CleanShot 2024-02-03 at 13.14.41@2x.png]]
`<label for="id 값">`에 지정된 `id`가 체크박스에서 동적으로 생성된 `regions1`, `regions2`, `regions3`에 맞추어 순서대로 입력된 것을 확인할 수 있다.
