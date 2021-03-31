# 서블릿이란?

### 💡 CGI -> Servlet -> JSP

<br>

## **CGI(Common Gate Interface)**

> 웹 서버와 동적 컨텐츠를 제공하는 프로그램 사이 규약

&nbsp; 웹서버는 정적인 컨테츠만 제공할 수 있다. 하지만 사람들은 자신의 계정으로 로그인하여 자신만의 정보 확인하는 동적인 컨텐츠를 원했다. 그래서 동적 컨텐츠를 생성할 수 있는 프로그램을 만들고 이 프로그램과 웹서버간 데이터를 주고 받을 수 있는 규격인 CGI가 만들어졌다.

## **서블릿의 탄생 배경**

<img src="https://user-images.githubusercontent.com/70243735/113125629-c29ce300-9251-11eb-8675-228991956f48.PNG" width="550px">

&nbsp; 초창기 CGI는 주로 C나 Perl를 사용해서 위의 그림처럼 구현하였는데 이 방법은 많은 사용자를 처리하기엔 무리가 있었다.

- 프로세스의 사용

    하나의 Request마다 스레드가 아닌 프로세스를 사용하여 메모리를 많이 차지하고 있었다.

- 동일 구현체를 여러번 생성

    동일한 구현체를 사용해도 Request(프로세스, 스레드)마다 CGI구현체를 각각 생성해야했다.

이런 문제점을 해결하고자 스레드와 싱글톤 패턴을 사용하는 서블릿이 탄생하게되었다.

<br>

## **서블릿(Servlet)**

> 클라이언트 요청에 따라 동적으로 컨텐츠를 생성하는 자바 클래스

<img src="https://user-images.githubusercontent.com/70243735/113125982-26bfa700-9252-11eb-8480-2d5a8724dc74.PNG" width="550px">

서블릿은 프로그램이 실행될때 스레드단위로 실행되어 서버의 부하를 줄였다. 

### **[ 서블릿의 동작 방식 ]**

<img src="https://user-images.githubusercontent.com/70243735/113126098-448d0c00-9252-11eb-9c53-d942b73d51ef.PNG" width="700px">

1. 서블릿컨테이너가 HttpServletRequest, HttpServletResponse 객체를 생성한다.
2. web.xml을 기반으로 사용자가 요청한 url이 어느 서블릿에 대한 요청인지 찾는다.
3. 해당 서블릿에서 service메소드를 호출한 후, 클라이언트의 호출에 맞게 doGet()또는 doPost()를 호출한다.
4. doGet() 또는 doPost()는 동적페이지를 생성하고 HttpServletResponse객체에 응답을 보낸다.
5. 응답이 끝나면 HttpServletRequest, HttpServletResponse 객체를 소멸시킨다.

<br>

## **JSP**

> Java 코드가 들어가 있는 HTML코드

 &nbsp; 서블릿은 **HTML코드가 있는 Java코드**인 반면 JSP는 **Java코드가 있는 HTML코드**이다. 서블릿의 경우 HTML형식으로 출력하기위해 print()메소드를 사용하여 일일이 String으로 태그들을 양식에 맞춰써야해서 불편함이 있었다. HTML표준을 따른 JSP를 사용하게되었고 비지니스로직과 프레젠테이션 로직을 분리시킬 수 있었다.

 JSP는 서블릿 컨테이너에 의해 서블릿 클래스로 변환되어 사용된다.

<br>

참고 출처:   
[https://youtu.be/2pBsXI01J6M](https://youtu.be/2pBsXI01J6M)   
https://mangkyu.tistory.com/14