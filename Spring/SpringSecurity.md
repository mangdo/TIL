# Spring Security

&nbsp; 스프링 시큐리티는 인증 및 권한 부여를 제공하는 스프링 하위 프레임워크이다. 사실상 spring 기반 애플리케이션 보안을 위한 표준이라고 [spring 공식 사이트](https://spring.io/projects/spring-security)에서 소개하고 있다.

## **동작 방식**
> 스프링 시큐리티의 기본 동작 방식은 서블릿의 여러 필터와 인터셉터를 이용해서 처리된다.

&nbsp; 필터(filter)와 인터셉터(interceptor)는 특정한 서블릿이나 컨트롤러의 접근에 관여한다는 점에서 유사하지만, **필터**는 스프링과 무관한 **서블릿 자원**이고 **인터셉터**는 **스프링의 빈**으로 관리되면서 스프링의 컨텍스트 내에 속한다는 차이이다. 필터는 스프링과 무관하지만 인터셉터는 스프링 내부에서 컨트롤러를 호출할때 관여하기 때문에 스프링의 컨텍스트 내에 있는 모든 자원을 활용할 수 있다. 때문에 적용 시기에서도 차이가 보인다. 필터는 디스패처 서블릿으로 가기 전에 적용되어 가장 먼저 URL 요청을 받지만 인터셉터는 디스패처와 컨트롤러 사이에 위치하여 적용된다.

<img src="https://user-images.githubusercontent.com/70243735/113886040-52670200-97fb-11eb-9e66-7f99e66bb929.PNG" width="550px">

&nbsp; 스프링 시큐리티를 이용하게 되면 위의 그림과 같이 인터셉터와 필터를 이용하면서 **별도의 컨텍스트**를 생성해서 처리된다. 하나의 스프링 MVC 프로젝트에 스프링 스큐리티가 적용되면 다음과 같은 구조가 생성된다. 스프링 시큐리티는 현재 동작하는 스프링 컨텍스트 내에서 동작하기 때문에 이미 컨텍스트에 포함된 여러빈들을 같이 이용해서 다양한 방식의 인증처리가 가능하도록 설계할 수 있다.

<br>

<img src="https://user-images.githubusercontent.com/70243735/113886882-fa7ccb00-97fb-11eb-8d72-a26e13461366.PNG" width="450px">

&nbsp; 스프링 시큐리티에서는 인증과 권한부여와 관련된 기능을 제공한다. **인증은 자기자신을 증명**하는 것이고 **권한부여(인가)는 인증을 한다음에 남에게 의해서 자격(권한)을 부여받는** 것이다.

스프링시큐리티에서 인증을 담당하는 AuthenticaionManager는 가장 핵심적인 역할을 하는 존재이기도 하다.

<br>

핵심적인 기능을 하는 요소들을 하나씩 알아보면 다음과 같다.

+ **AuthenticationManager**(인증 관리자)를 구현한 providerManager는 authenticaionProvider라는 타입의 객체를 이용해서 처리를 위임한다.
+ **AuthenticaionProvider**(인증 제공자)는 실제 인증 작업을 진행한다. 사용자가 인증 요청한 정보와 DB의 사용자 정보가 일치하는지를 확인한다.
+ **UserDetailsService**는 DB의 사용자 정보를 조회한다
+ **UserDetails**는 조회한 사용자 정보를 담는 인터페이스이다.

<br>

## **인증 과정**
<img src="https://user-images.githubusercontent.com/70243735/113887618-9c9cb300-97fc-11eb-8535-07a77dea5998.PNG" width="550px">


1. 사용자가 아이디, 비밀번호로 인증을 요청한다.

    : 들어오는 각 요청은 인증 및 권한 부여 프로세스를 위해 일련의 필터를 거친다.

2. AuthenticationFilter에서 UsernamePasswordAuthenticationToken을 생성한다.

    : 사용자 이름과 비밀번호를 기반으로 인증 객체이다.

3. 생성한 토큰을 AuthenticationManager(인증 관리자)에게 전달한다.

4. AuthenticaionManager는 등록된 AuthenticaionProvider들(인증 제공자)을 조회하여 인증을 요구한다.

5. 입력받은 비밀번호를 암호화한다.

6. AuthenticationProvider는 UserDetailsService를 통해 입력받은 아이디에 대한 사용자 정보를 DB에서 조회한다.

7. DB에서 조회한 사용자의 정보를 UserDetails에 담는다.

8. UserDetailsService가 AuthenticationProvider에게 DB에서 조회한 사용자의 정보를 반환한다.

9. 암호화된 비밀번호와 DB의 비밀번호와 매칭이 되면 인증이 성공된 UsernameAuthenticationToken을 생성하여 AuthenticaionManager로 반환한다.

10. AuthenticaionManager는 UsernameAuthenticaionToken을 AuthenticaionFilter로 전달한다.

11. AuthenticationFilter는 전달받은 UsernameAuthenticationToken을 LoginSuccessHandler로 전송하고, SecurityContextHolder에 저장한다.

 

<br>
<br>

+ 개발자가 스프링 시큐리티를 커스터마이징하는 방식

AuthenticationProvider를 구현하는 방식 : 새로운 프로토콜이나 인증 구현방식을 직접 구현할때
UserDetailService를 구현하는 방식 : 대부분의 경우

<br>
참고 출처 :

코드로 배우는 스프링 프레임워크   
www.techtalks.lk/blog/2018/10/spring-security-authentication   
www.javadevjournal.com/spring-security/spring-security-authentication/