```java
package org.springframework.core.convert.converter;

public interface Converter<S, T> {
	T convert(S source)
}
```
스프링은 확장 가능한 컨버터 인터페이스를 제공하며, 개발자는 추가적인 타입 변환이 필요한 경우, 컨버터 인터페이스를 구현해서 등록하면 된다.

- 컨버터 인터페이스는 모든 타입에 적용할 수 있다.
	- `X -> Y` 타입으로 변환하는 컨버터 인터페이스를 수현하고, 또 `Y -> X` 타입으로 변환하는 컨버터 인터페이스를 등록하면 됨.
- 예를 들어, `"true"`가 왔을 때, Boolean 타입으로 변환하는 경우, `String -> Boolean` 타입으로 변환하도록 컨버터 인터페이스를 구현하고 등록, 반대의 경우는 `Boolean -> String` 타입으로 처리.
