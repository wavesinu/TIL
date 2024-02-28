# Entity / Attribute / Entity Set
DB는 개체들의 집합과 개체들 간의 관계로 모델링 할 수 있음.
### Entity
Entity란, 다른 객체와 구별되어 존재하는 하나의 객체를 뜻함. 예를 들어 사람이나 책처럼 구체적인 것이 될 수도 있고, 수업이나 예약처럼  추상적인 것도 엔티티가 될 수 있음.
### [[Attribute]]
모든 Entity들은 `attribute`를 가지고 있다. `attribute는` 값을 가지고 있고, 각 entity는 `attribute에` 대한 자신만의 값을 가짐.
`attribute는` 어떤 `entity` 집합의 구성원들이 공통적으로 가지는 특징을 표현함.
해당 집합의 attribute들로 각 enitty를 고유하게 식별할 수 있게 됨.
### Entity Set
`Entity Set`는 같은 attribute를 가지고 있는 entity들의 집합임. (=`relation`)
entity set은 서로 중복될 수 있음. 예를 들어 person은 student이거나 instructor가 될 수 있음.
- E-R Diagram에서 직사각형으로 표현된다.
- 개체들로 구성된 집합이다.
- key 역할을 할 수 있는 Attribute는 밑줄을 그어 표시한다.
- Key 역할을 할 수 있는 Attribute들을 Candidate라 부르고, 다수의 Candidate가 존재하는 경우, 그 중 하나를 Primary Key로 지정한다.
- 개체집합 내에 모든 객체들은 같은 Attribute Set을 가지고 있다.
# Relationship / Relationship Set
![[Pasted image 20240127003936.png]]
### Relationship
`Relationship`이란 entity 간 의미 있는 연관성을 의미함. 즉, entity들이 어떻게 서로 연관되어 있는지를 말함.
- 둘 이상의 개체들 간의 관련성이다.
- Entity Set 간의 관계를 나타낸다.
- 관계에도 Attribute가 존재할 수 있으며, 이를 Relationship Attribute라고 한다.
- 하나의 Entity Set 내에서의 Relationship을 Unray Relationship이라고 한다.
- 두 개의 Entity Set 사이의 Relationship을 Binary Relationship이라고 한다.
- 세 개의 Entity Set 사이의 Relationship을 Ternary Relationship이라고 한다.
### Relationship Set
`Relationship`은 각 entity들의 관계를 뜻하고, `Relationship Set`은 이러한 Relationship의 집합을 뜻함.
![[Pasted image 20240127003946.png]]
- Relationship Set은 `Attribute`를 가질 수 있다. 
	- instructor(좌)와 student(우) entity들 간에는 advisor라는 Relationship set을 가지는데, advisor는 Date라는 `Attribute`를 가진다.
- E-R Diagram에서 마름모로 표현된다.
- 관계집합은 개체와, 개체가 속한 개체집합 쌍으로 구성된 N개의 Tuple로 구성된다.
- 관계집합은 Descriptive Attribute를 가질 수 있다.

> **Descriptive Attribute**
> 한 개체에 관한 정보보다는, 관계에 관한 정보를 기술하는 속성

### Relationship Set의 Key
![](https://velog.velcdn.com/images%2Fyohanblessyou%2Fpost%2F85836f42-10ca-434c-8b38-eab40c41eead%2Fimage.png)
- Relationship Set에도 각 Relation을 구분하기 위한 `Key` 개념이 존재함. Relationship Set의 key는 참여하는 entity set의 key들을 사용해 만들게 됨.
	- 위는 student의 s_id와 instructor의 i_id의 조합이 advisor라는 Relationship set의 superkey로 선정한 예시
### Relationship Set의 Degree 개념
![[Pasted image 20240127005353.png]]
Relationship Set에는 `Degree(차수)` 개념이 있으며, 해당 Relationship Set에 참여하는 entity set의 개수를 말함.
이전 예시에서 instructor와 student 간의 advisor 관계는 두 개의 entity set만 참여하므로 `binary relationship`이라고 하며, 대부분의 관계는 binary로 되어 있음.

---

