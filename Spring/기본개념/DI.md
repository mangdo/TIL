# DI의 세가지 방법

&nbsp; 마틴파울러는 IoC에서 DI라는 개념을 구체화시키면서 DI에 대한 3가지 방법을 제시하였다.

*Forms of Dependency Injection*   
 &nbsp; *There are three main styles of dependency injection. The names I'm using for them are Constructor Injection, Setter Injection, and Interface Injection.*
<[https://martinfowler.com/articles/injection.html](https://martinfowler.com/articles/injection.html)>   

<br>

----

<br>

### **강한 결합**

객체 내부에서 다른 객체를 생성하는 것은 강한 결합도를 가지는 구조이다. A클래스에서 B객체를 직접 생성해서 사용한다면 B객체를 수정하려면 A클래스도 수정해야하는 방식이기에 강한 결합이다.

### **느슨한 결합**

객체를 주입 받는다는(DI) 것은 외부에서 생성된 객체를 인터페이스를 통해서 넘겨받는 것이다. 이렇게 하면 결합도를 낮출 수 있고, **런타임시에 의존관계가 결정**되기 때문에 **유연한 구조**를 가진다.

<br>

## 필드 주입 (Field Injection)

```java
public  class  ExampleController {
    @Autowired
    private FirstService firstService;
		@Autowired
    private SecondService secondService;
}
```

## 수정자 주입(Setter Injection)


```java
public  class  ExampleController {
    
    private FirstService firstService;
    private SecondService secondService;
    
    @Autowired
    public void setFirstService(FirstService firstService){
   	    this.firstService = firstService;
    }

	@Autowired
    public void setSecondService(SecondService secondService{
   	    this.firstService = firstService;
    }
}
```
롬복을 이용한다면 더 간단하게 작성할 수 있다.

```java
public  class  ExampleController {
    @Setter(onMethod_=@Autowired)
    private FirstService firstService;
	
    @Setter(onMethod_=@Autowired)
    private SecondService secondService;
}

```

<br>

## 생성자 주입(Constructor Injection)

> Spring에서 권장하는 방식.

&nbsp; Spring 3.x 버전까지만 해도 Setter Inject을 권장하였으나, 최근에는 순환참조, Coupling등이 문제로 인해서 Spring 4.3 이후 버젼 부터는 생성자 주입을 권장하고 있다.

```java
public  class  ExampleController {
    
    private  final  FirstService firstService;
    private  final  SecondService secondService;
    
    @Autowired
    public ExampleController(FirstService firstService, SecondService secondService){
   	this.firstService = firstService;
		this.secondService = secondService;
    }
}
```

spring 4.2부터 단일 생성자일 경우에는 **@Autowired를 생략 가능**하다.

&nbsp; 다만, 생성자가 여러개일 경우 compile error가 발생하기때문에 특정 생성자에 @Autowired를 붙여줘야한다. (@AllArgsConstructor @RequiredArgsConstructor를 같이쓰면 에러가 발생! 주의!)

&nbsp; 생성자를 직접 만드는것이 번거로울 수 있다. 이때는 롬복을 사용하면 훨씬편하게 만들 수 있다. 롬복의 @RequiredArgsConstructor를 쓰면 훨씬 간단하게 할 수 있다.

```java
@RequiredArgsConstructor
public  class  ExampleController {

    private  final  FirstService firstService;
    private  final  SecondService secondService;

}
```

<br>

## 생성자 주입을 권장하는 이유?

1. final 사용 가능

     : final 키워드는 선언과 함께 반드시 초기화가 되어야한다. 때문에 Setter와 필드 주입은 final사용이 불가능하다. 그래서 주입받는 객체가 변경될 수 있는 가능성이 있다.

2. 의존성을 외부로 노출

    : Setter와 필드 주입은 주입되어야할 객체가 없어도 객체가 생성이 가능하다. 생성 후, 해당 객체를 사용하는 시점에 NullPointerException을 발생시킨다. 하지만 생성자주입은 **주입되어야할 객체가 없다면** 생성 자체를 시키지않는다. 즉, **의존관계에 대한 내용을 외부로 노출**시켜 **컴파일 타임에 오류**를 잡아낼 수 있다.

3. 순환참조 방지

    : 비지니스 로직상에서 FirstService가 SecondService를 참조하고 SecondService가 FirstService를 참조하는 경우가 생길 수 있다. 필드 주입이나 Setter주입은 객체 생성시점에 순환참조가 일어나는지 아닌지를 발견할 수 없다. 그래서 객체를 사용하는 시점에 StackOverflowError를 발생시키게된다. 하지만 **생성자 주입은 순환참조가 있다면 어플리케이션 구동 자체가 불가능**해서 미리 알아낼 수 있다.

4. 단위테스트 가능

    : 필드 주입을 사용하면 Spring 컨테이너가 아닌 외부에서의 주입이 불가능하다. 즉, 필드 주입을 사용한 클래스라면 의존성이 있는 객체를 주입시킬 수 없어 단위 테스트 불가능하다.