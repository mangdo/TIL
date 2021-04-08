# IoC vs DI

> &nbsp; IoC는 Spring에서 시작된 용어가 아닌 과거에서부터 존재하던 소프트 디자인 패턴 중 하나이다. Spring Framework는 바로 이 IoC를 DI라는 방식으로 구현하였다.

<br>

## IoC(Inversion of control)

> 제어의 역전, 즉 외부에서 제어를 한다는 뜻이다. 

&nbsp; 개발자(코드)가 더이상 객체의 생성, 관계설정, 소멸까지의 생명주기 관련된 모든 관리를 해주지 않아도 된다는 의미이다.

<br>

## 스프링 컨테이너? IoC컨테이너?

&nbsp; 스프링 프레임워크에서는 객체의 생성과 , 관계설정, 소멸까지의 생명주기관련된 모든 관리를 어플리케이션 코드가 아닌 독립된 컨테이너가 담당한다. 때문에 [스프링 컨테이너](./SpringContainer.md)를 **개발자(코드)대신 객체에 대한 제어권을 가지고 있다고 하여 IoC컨테이너라고도 한다.**

<br>

## IoC vs DI

&nbsp; 스프링 프레임워크의 가장 큰 장점으로 IoC컨테이너 기능이 부각되어 있으나, IoC는 너무 포괄적인 개념이기도 하고 스프링 프레임워크가 탄생하기 훨씬 전 부터 사용되던 디자인 패턴이였다.

*"As a result I think we need a more specific name for this pattern. Inversion of Control is too generic a term, and thus people find it confusing. As a result with a lot of discussion with various IoC advocates we settled on the name Dependency Injection."*   
*"결과적으로 이 패턴에 대한 구체적인 이름이 필요하다고 생각했습니다. IoC는 너무 포괄적인 용어이기에 사람들에게 혼란을 줄 수 있습니다. 많은 토의 끝에 우리는 Dependency injection이라는 이름을 정했습니다."*


출처 : [마틴파울러의 IoC와 CI에 대한 글](https://martinfowler.com/articles/injection.html)

<br>

## DI(Dependency Injection)
> 컨테이너(외부)에서 동적으로 의존성을 주입

&nbsp; 클래스 사이의 의존관계를 bean설정정보를 바탕으로 컨테이너가 자동적으로 연결해주는것을 말한다. 개발자들은 제어를 담당할 필요없이 bean 설정파일에 의존관계가 필요하다는 정보만 추가하면된다. 그러면 오브젝트 레퍼런스를 컨테이너로 **(외부)부터 주입** 받아서 , **실행 시에 동적으로 의존관계가 생성**된다. 즉 컨테이너가 Control의 주체가 되어 애플리케이션 코드에 의존관계를 주입시켜준다.

### **DI의 장점?**

- 유연한코드

: 코드에서 비지니스 로직 뿐만아니라 객체의 생성, 소멸, 의존관계까지 들어가게되면 의존적인 코드가 될 수 있다.

- 개발자가 비지니스 로직에만 집중할 수 있게함


<br>

참고 출처:   
[https://www.nextree.co.kr/p11247/](https://www.nextree.co.kr/p11247/)   
[https://biggwang.github.io/2019/08/31/Spring/IoC, DI란 무엇일까/#undefined](https://biggwang.github.io/2019/08/31/Spring/IoC,%20DI%EB%9E%80%20%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C/#undefined)   
[https://limmmee.tistory.com/13](https://limmmee.tistory.com/13)    
[https://sallyhan82.tistory.com/4](https://sallyhan82.tistory.com/4)