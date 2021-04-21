# JAR vs WAR 

<img src="https://user-images.githubusercontent.com/70243735/115487165-1750de00-a293-11eb-88a2-690c7f3006e4.png" width ="450px">

## [ JAR ]
> 자바프로젝트 압축 파일포맷

Java Archive   
**자바 클래스** 파일과 클래스가 이용하는 관련 리소스 및 메타 데이터를 모아서 배포하기 위한 소프트웨어 패키지 파일포맷이다.
- 원하는 구조로 구성 가능
- JRE(Java Runtime Envirment)만 가지고도 실행 가능

<br>

## [ WAR ]
> 웹 어플리케이션 압축 파일포맷

Web application Archive   
&nbsp; Servlet/Jsp 컨테이너에 배치할 수 있는 웹 어플리케이션 압축 파일 포맷이다. JSP, Servlet, Class, XML, HTML, Javascript 및 **웹 애플리케이션을 함께 이루는 자원**들을 모아 배포하는 데 사용된다. 즉, 웹 관련된 자원들만 포함하고 있어 웹 애플리케이션의 간편한 배포를 도와준다.
- WEB-INF, META-INF구조를 따라야한다.
- 웹서버나 WAS가 있어야 실행 가능

<br>

## [ 스프링부트과 JAR, WAR ]

JSP파일을 사용한다면 JAR가 아닌 WAR를 사용해야 한다.  
또한, 일반적으로 외장 WAS를 사용하는 경우에는 WAR파일을, 내장 WAS를 사용하는 경우 JAR파일을 사용한다고 한다.

&nbsp; 스프링 부트의 장점으로 꼽히는 것들 중 하나에는 '**JAR파일로 간단하게 배포 가능**하다'라는 것이 있다. 스프링 부트는 **톰캣을 JAR에 내장**하기 때문에 바로 실행가능한 JAR파일로 빌드와 배포가 가능하다. 독립적이고 가볍게 만들 수 있는 것이다.   
&nbsp; 스프링 부트를 사용하여 JAR파일로 빌드, 배포할때는 AWS EC2서버에 JDK 1.8만 설치해도 된다. 하지만 스프링은 WAR파일로 빌드, 배포하기 때문에 EC2 서버에 tomcat도 설치해야한다.