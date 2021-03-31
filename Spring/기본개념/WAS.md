# WAS와 Web Server, Web Container


<img src="https://user-images.githubusercontent.com/70243735/113125026-21ae2800-9251-11eb-9c98-bb56279067aa.PNG" width="550px">

## Web Server?

클라이언트의 요청을 받아 **정적인 컨텐츠**를 응답하는 서버   
ex) Apache

## WAS? 

클라이언트 요청을 받아 **동적인 컨텐츠**를 응답하는 서버   
&nbsp; 대부분의 WAS는 정적인 컨텐츠를 제공해주기 때문에 WAS는 웹서버를 포함하는 개념이다. WAS는 크게 WebServer와 Web Container로 구성된다. 

## Web Container?

&nbsp; Web Server가 **정적으로 처리해야할 데이터를 제외한 JSP, 서블릿클래스등을 요청받았다면** 이를 웹 컨테이너에서 처리하도록 넘겨준다. 웹 컨테이너에서는 요청받은 서블릿 클래스, JSP 파일을 실행하여 그 결과를 다시 WebServer로 넘겨주고 이는 응답 메시지 형태로 사용자의 브라우저에 전송된다.

&nbsp; 웹 컨테이너 안에 JSP 컨테이너, Servlet 컨테이너, EJB컨테이너가 있다. (아파치 톰캣은 EJB컨테이너 기능 구현x)

&nbsp; 서블릿 클래스에 대한 웹 컨테이너를 서블릿 컨테이너, JSP 파일에 대한 웹 컨테이너를 JSP 컨테이너라고 한다. 다만 실제적으로 이 둘을 혼용하여 **웹 컨테이너**(**서블릿 컨테이너**)로 통칭하는 경우가 많다. 

ex) 톰캣, 웹로직, Resin 등이 있다.

<br>

## 아파치 톰캣은?

&nbsp; 톰캣은 서블릿컨테이너(또는 웹컨테이너)만 있는 웹 어플리케이션 서버라고 한다.([https://ko.wikipedia.org/wiki/아파치_톰캣](https://ko.wikipedia.org/wiki/%EC%95%84%ED%8C%8C%EC%B9%98_%ED%86%B0%EC%BA%A3))
톰캣을 정확하게 구분지어 말하기 보다는 <u>WAS, 웹 컨테이너, 서블릿 컨테이너라고 부른다</u>.

&nbsp; 톰캣은 아파치와 합쳐서 아파치톰캣이라고 불리는데 톰캣이 아파치의 기능 일부를 가져와서 제공해줘서 부르기도 하고 실제로 아파치를 앞에 두기때문에 아파치톰캣이라고도 부른다.

* 아파치만 두면?   
&nbsp; 정적인 페이지만 처리가능하다.

* 톰캣만 사용하면?   
&nbsp; 동적인 페이지 처리까지 가능하지만 여러 사용자의 요청이 있을시에 **톰캣에 과부하**가 걸릴 수 있다.

* 아파치와 톰캣을 같이 쓰면?!  
&nbsp; **아파치는 정적인 데이터만 처리하고 JSP처리는 WebContainer(톰캣의 일부)로 보내주어 분산처리** 할 수 있다.


<br>

참고 출처   
[https://pjh3749.tistory.com/267](https://pjh3749.tistory.com/267)   
[https://mangkyu.tistory.com/14](https://mangkyu.tistory.com/14)   
[https://m.blog.naver.com/PostView.nhn?blogId=youhr21&logNo=221542836167&proxyReferer=https:%2F%2Fwww.google.com%2F](https://m.blog.naver.com/PostView.nhn?blogId=youhr21&logNo=221542836167&proxyReferer=https:%2F%2Fwww.google.com%2F)   
모델 2로 구현하는 자바 웹 프로그래밍 JSP 2.2 & Servlet 3.0, 오정원 저, 혜지원