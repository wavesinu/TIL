# MSA란?
![[CleanShot 2024-02-29 at 00.53.13@2x.png]]
MSA(Micro Service Architecture)는 [[SOA]]의 경량화 버전으로, 모놀리틱 아키텍처를 나눠서 독립적으로 구분한다. Microservice는 독립적으로 배포 / 확장 될 수 있는 서비스들을 조합하여 더 큰 어플리케이션을 구성하는 아키텍처 패턴이다.

MSA는 일반적으로 다음의 서비스들의 조합으로 이루어져있다.
1. [[Service Discovery]]
2. [[API Gateway]]
3. [[Orchestration]]
4. [[Choreography]]
5. [[Context Boundary]]

# MSA 특징
MSA는 API를 통해서만 상호작용할 수 있다. 즉, 마이크로 서비스는 서비스의 end-point를 API 형태로 외부에 노출하고, 실질적인 세부 사항은 모두 추상화한다.
내부의 구현 로직, 아키텍처와 프로그래밍 언어, 데이터베이스, 품질 유지 체계와 같은 기술적인 사항들은 서비스 API에 의해 가려진다.

이러한 방식을 통해 마이크로서비스 간의 결합도를 낮추고 유연성을 높일 수 있으며, 각 마이크로 서비스는 자신의 API를 통해 외부에 서비스를 제공하므로, 변경이 필요할 때 다른 서비스에 영향을 미치지 않고 해당 서비스만 수정할 수 있다.
>MSA는 서비스 소비자와 서비스 제공자 사이의 데이터 교환을 위해 HTTP, JSON과 같은 경량 통신 프로토콜을 사용한다.

- 마이크로 서비스는 [[SOA]]에서 사용되는 집중화된 관리 체계를 사용하지 않는다.
- 마이크로 서비스 구현체의 특징 중 하나는 ESB와 같은 무거운 제품에 의존하지 않는다는 점이다.
	- REST와 같은 경량 통신 아키텍처 또는 Kafaka 등을 이용한 message stream을 주로 사용한다.
# MSA의 장점
- 각각의 서비스가 모듈화 되어있으며, 모듈끼리 RPC 또는 message-driven API 등을 사용하여 통신하기 때문에, 개별적인 서비스 개발 속도가 높고 유지보수가 용이하다.
- MSA는 각 마이크로 서비스가 독립적으로 개발되고 배포되기 때문에 각 마이크로 서비스가 자체적인 기술 스택을 가질 수 있다.
- 마이크로 서비스는 각 서비스의 부하에 따라 개별적인 scale-out이 가능하다.
>##### 스케일 아웃(scale-out)이란?
>시스템의 부하에 따라 필요한 서비스 인스턴스의 수를 조정하는 것을 말함.
# MSA의 단점
- MSA는 여러 개의 독립적인 마이크로 서비스로 구성되기 때문에 전체적인 시스템의 복잡성이 증가한다.
- 각 마이크로 서비스는 서로 다른 DB를 가질 수 있기 때문에 트랜잭션의 유지가 어렵다.
	- 이벤트 소싱 패턴([[Event Sourcing pattern]]) 또는 [[CQRS]] 패턴을 사용하여 데이터 일관성을 보장하고 트랜잭션을 분산적으로 처리할 수 있다.

---
### 참고 자료
- [[MSA] MSA란 무엇인가? 개념 이해하기 (tistory.com)](https://wooaoe.tistory.com/57)
- [[MSA 개념 정립하기] MSA의 개념과 장단점 (tistory.com)](https://waspro.tistory.com/429)
- [마이크로 서비스 아키텍처 스타일 - Azure Architecture Center | Microsoft Learn](https://learn.microsoft.com/ko-kr/azure/architecture/guide/architecture-styles/microservices)
