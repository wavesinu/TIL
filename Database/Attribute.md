entity는 `Attribute`의 집합으로 표현할 수 있다. attribute는 해당 entity set의 모든 멤버가 가지고 있는 특성을 말함.
### Domain
`Domain`이란, 각 attribute에 허용되는 값들의 집합을 뜻함.
### Attribute type
`Attribute type`에는 다음과 같은 종류가 있음.
- **Simple vs Composite**
	Simple attribute는 더 이상 작은 단위로 나눠지지 않는 값을 가지는 경우를 말하고, 반대로 Composite attribute는 더 작은 단위/속성으로 나눠질 수 있는 경우
- **Single-valued vs Multi-valued**
	Single-valued attribute는 특정 entity에 대해 하나의 값만 가지고, Multi-valued는 한 번에 여러 개의 값을 가질 수 있는 경우. (ex. 연락처 attribute에는 집전화/휴대폰 등 여러 개가 올 수 있음)
- **Derived**
	직접 저장되지 않고 필요할 때마다 다른 attribute을 이용하여 계산되는 경우 (Swift의 computed 프로퍼티 느낌)

![[Pasted image 20240127132555.png]]
>`Composite` Attribute를 살펴보면, 이는 경우에 따라 해당 속성 값의 전체 혹은 일부만을 참조하고 싶을 때 유용하다. 
>예를 들어, name이라는 attribute는 풀네임을 필요할 때도 있지만 first name만 필요한 경우도 존재한다. 또한 address처럼 계층 구조를 가질 수 있어 모델링을 더 명확하게 할 수 있고, 연관된 attribute들을 하나의 그룹으로 묶을 수 있다는 장점이 있다.

