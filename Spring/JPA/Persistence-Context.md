# 영속성 컨텍스트

<br>

## 💡 영속성 컨텍스트란?

&nbsp; 영속성 컨텍스트는 엔티티를 영속화 합니다. 즉, 엔티티를 영구적으로 저장해주는 환경을 의미합니다.

&nbsp; 영속성 컨텍스트 논리적인 개념으로 눈에 보이지 않습니다. 엔티티 매니저를 하나 생성할 때 하나의 영속성 컨텍스트가 만들어지며 엔티티 매니저를 통해 접근하고 관리할 수 있습니다. 영속성 컨텍스트를 쓰는 이유는 1차 캐시, 동일성 보장, 쓰기 지연, 변경감지(Dirty checking), 지연로딩이 있습니다

 <br>

## 💡 영속성 컨텍스트의 장점

- **1차 캐시**<br>
    : 영속성 컨텍스트의 내부에 존재하는 캐시를 1차 캐시라고 합니다.<br>
    : find()함수를 호출하게 되면 우선 1차 캐시에서 조회하고, 없으면 DB에서 조회한 다음에 1차 캐시에 저장합니다. 만약 1차 캐시에 있다면 DB까지 조회할 필요 없이 1차 캐시에서 바로 찾아서 반환합니다.
    
- **동일성 보장** <br>
    : 동일성 비교가 가능합니다.(==)

    ```java
    Person minseo = new Person("minseo");
    entityManger.persist(minseo);

    // 조회
    Person person1 = entityManger.find(Person.class, 1);
    Person person2 = entityManger.find(Person.class, 1);

    System.out.println(person1 == person2); // true

    ```

- **쓰기 지연**<br>
    : 트랜잭션 커밋하기 전까지 SQL들을 영속성 컨텍스트의 SQL저장소에 모았다가 한번에 보낼 수 있습니다.
    
- **Dirty checking**<br>
    : 1차 캐시에 들어온 데이터에 대해 스냅샷을 찍습니다. <br>
    : 트랜잭션이 commit 되는 시점에 Entity와 스냅샷과 비교하여 update 쿼리를 자동 생성합니다.
 
- **Lazy Loading**<br>
    : 실제 객체 대신 프록시 객체를 로딩해두고,  해당 객체를 실제로 사용할 때, SQL을 날려 데이터를 가져옵니다.
    
<br>
<br>

Refernce :<br>
인프런 강의 - 김영한님의 자바 ORM 표준 JPA 프로그래밍<br>
[[JPA] 영속성 컨텍스트1 - 엔티티 생명주기](https://doing7.tistory.com/110)<br>
[[Spring] 영속성이란 (persistence)](https://hyeooona825.tistory.com/87)<br>