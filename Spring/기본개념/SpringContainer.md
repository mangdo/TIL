# Spring Container

## **IoC컨테이너**
&nbsp; 스프링 프레임워크에서는 객체의 생성과 , 관계설정, 소멸까지의 생명주기관련된 모든 관리를 어플리케이션 코드가 아닌 독립된 컨테이너가 담당한다. 때문에 스프링 컨테이너를 **개발자(코드)대신 객체에 대한 제어권을 가지고 있다고 하여 IoC컨테이너라고도 한다.**

## **Bean Factory**
> 스프링 컨테이너에 접근하기 위한 최상위 인터페이스

&nbsp; 빈(Bean)이란, **스프링이 제어권을 가지고** 직접 만들고 관계를 부여하는 오브젝트를 말한다. 즉 빈은 스프링 컨테이너가 생성과 관계설정, 사용등을 제어해주는 오브젝트이다. 스프링에선 IoC컨테이너를 빈 팩토리 또는 애플리케이션 컨텍스트라고 부르기도 한다. Bean Factory라고 말할때는 빈을 생성하고 관계를 설정하는 IoC기본 기능에 초점을 맞춘것이고 Application Context라고 말할때는 애플리케이션 전반에 걸쳐 모든 구성요소의 제어 작업을 딤당하는 IoC엔진이라는 의미가 부각된다.

<br>

## **Application Context**
> Bean Factory 인터페이스를 상속한 서브 인터페이스

&nbsp; 스프링 컨테이너는 단순한 DI 작업보다 다양한 일을 한다. DI를 위한 Bean Factory에 엔터프라이즈 애플리케이션을 개발하는 데 필요한 여러가지 컨테이너 기능을 추가한 것을 Application Context라고 한다. ApplicaionContext에서는 설정 메타정보를 참고해서 Bean의 생성, 관계 설정 뿐만아니라 오브젝트가 만들어지는 방식, 시점, 전략등을 다르게 가져가서 다양한 기능을 제공한다. DI 작업을 포함하여 애플리케이션 전반에 걸친 제어작업을 총괄한다.    
&nbsp; 실제로 스프링 컨테이너 또는 IoC컨테이너라고 말하는 것은 바로 이 **Application Context 인터페이스를 구현한 클래스의 오브젝트**이다. 스프링 애플리케이션은 최소 하나 이상의 IoC 컨테이너, 즉 ApplicationContext 인터페이스를 구현한 클래스의 오브젝트이다.

<br>

## **IoC컨테이너로 애플리케이션 만들기**

IoC 컨테이너를 만드는 가장 간단한 방법은 ApplicaionContext를 구현한 클래스의 인스턴스를 만드는 것이다.

```java
StaticApplicationContext ac = new StaticApplicationContext();
```
&nbsp; StaticApplicationContext는 ApplicationContext를 구현한 클래스이다. 이로써 IoC컨테이너가 만들어졌지만 아직 빈 컨테이너 일뿐이다. 이렇게 만들어진 컨테이너가 본격적인 IoC 컨테이너로 동작하기 위해서는 POJO 클래스와 설정 메타정보가 필요하다.

* **POJO**(Plain Old Java Object)   
    : 특정 기술과 환경에 의존하지 않고 객체 지향적인 원리에 충실하게 만들어진 오브젝트. 객체 지향 언어인 Java의 장점을 살리는 오래된 방식의 순수한 자바 객체를 말한다. (재사용성, 확장성, 유지보수)

* **설정 메타정보**   
    : Bean을 어떻게 만들고 동작할 것에 대한 정보이다.   
    &nbsp; 스프링의 설정 메타정보는 XML파일이아닌 BeanDefinition 인터페이스로 표현되는 **순수한 추상정보**다. 스프링의 메타정보는 **특정한 파일 포맷이나 형식에 종속되지않는다.** BeanDefinition으로 정의되는 스프링의 설정 메타정보의 내용을 표현 한 것이라면 무엇이든 사용가능하다. 원본의 포맷과 구조, 자료의 특성에 맞게 읽어와 BeanDefinition 오브젝트로 변환해주는 **BeanDefinitionReader**가 있으면 된다. 이 Reader도 인터페이스 이므로 이를 구현한 리더만 만들면 스프링의 설정 메타정보는 어떤 형식으로든 작성할 수 있다.   
    ex) 빈 아이디(이름), 빈으로 만들 클래스 이름, 스코프, 프로퍼티 값

<br>
<img src="https://user-images.githubusercontent.com/70243735/114047948-1009f780-98c5-11eb-94b6-c74bb1a545e0.PNG" width="600px">

&nbsp; 스프링 IoC 컨테이너는 각 bean에 대한 정보를 담은 설정 메타정보를 읽어들인 뒤에 이를 참고해서 bean 오브젝트를 생성하고 프로퍼티나 생성자를 통해 의존 오브젝트를 주입해주는 DI 작업을 수행한다. 이런 작업을 통해 만들어진 bean들이 모여 하나의 애플리케이션을 구성하고 동작하게 된다.



<br>

참고 출처 :   
https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/BeanFactory.html   
https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/ApplicationContext.html   
토비의 스프링 3.1(이일민 저)