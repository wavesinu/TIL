# JPA란?
JPA(Java Persistent API)는 자바 플랫폼에서 [[ORM]]을 구현하기 위한 표준 인터페이스이며, JPA는 객체와 관계형 데이터베이스 간의 매핑을 위한 API를 정의한다.
# JPA는 기술 명세
JPA는 인터페이스이다. 즉, 특정 기능을 하는 라이브러리가 아니다. 일반적인 백엔드 API가 클라이언트가 어떻게 서버를 사용해야 하는지를 정의하는 것처럼, JPA 역시 자바 어플리케이션에서 관계형 데이터베이스를 어떻게 사용해야 하는지를 정의하는 한 방법일 뿐이다.

JPA의 구현체에는 [[Hibernate]]가 있다.
# Hibernate는 JPA의 구현체
JPA와 Hibernate는 자바의 `interface`와 해당 `interface`를 구현한 클래스와 같은 관게이다.
![[Pasted image 20240301122847.png]]
"**Hibernate는 JPA의 구현체이다**"로부터 도출되는 결론은 **JPA를 사용하기 위해 반드시 Hibernate를 사용할 필요가 없다는 것**이다.

# JPA 사용 이유
**ORM의 편의성**
- JPA를 사용하면 객체-관계형 데이터베이스 간의 매핑을 간편하게 처리할 수 있다.
- 개발자는 데이터베이스 스키마를 직접 작성하는 대신, JPA 어노테이션을 사용하여 객체와 테이블 간의 매핑을 정의할 수 있다.

**SQL 쿼리 작성의 간소화**
- JPA를 사용하면 SQL 쿼리를 직접 작성하지 않아도 된다.
- 대신 JPQL을 사용하여 객체를 검색하고 저장할 수 있으며, 이를 통해 개발자는 객체지향적인 쿼리를 작성하여 데이터를 다룰 수 있다.

**유지보수성 및 확장성 향상**
- JPA를 사용하면 객체 모델과 데이터베이스 스키마 간의 매핑을 한 곳에서 관리할 수 있으며, 이를 통해 객체와 데이터베이스 간의 일관성을 유지할 수 있다.
- JPA는 객체를 사용하여 데이터베이스를 다루기 때문에 코드의 가독성이 향상되고 유지보수가 용이해진다.

**표준화된 API**
- JPA는 자바 표준 API이므로 다양한 JPA 구현체(Hibernate, EclipseLink)에서 동일한 인터페이스를 사용할 수 있다. 이를 통해 구현체를 변경하더라도 코드 변경을 최소화 할 수 있다.
# JPA Annotation


---
### 참고 자료
[[Spring] JPA 개념정리 (Hibernate, Spring Data JPA) (tistory.com)](https://devmoony.tistory.com/186)
[JPA, Hibernate, 그리고 Spring Data JPA의 차이점 (suhwan.dev)](https://suhwan.dev/2019/02/24/jpa-vs-hibernate-vs-spring-data-jpa/)
[JPA 정의(Java Persistence API) / JPA 사용이유 / JPA 장단점 (tistory.com)](https://mkil.tistory.com/526)
