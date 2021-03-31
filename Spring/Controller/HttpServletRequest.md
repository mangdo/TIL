# HttpServletRequest


<img src="https://user-images.githubusercontent.com/70243735/113120165-4227b380-924c-11eb-9300-fe8280af9e96.PNG">


<br>
<br>

1. 웹 브라우저가 서버에 요청을 보낸다.

2. 서블릿 컨테이너가 HttpServletRequest라는 객체와 HttpServletResponse라는 객체를 생성

3. 생성된 두 개의 객체를 요청 정보에 있는 path로 매핑된 서블릿에게 전달

**HttpServletRequest**는 request 정보를 서블릿에게 전달한다.

**HttpServletResponse**는 서블릿 컨테이너는 요청을 보낸 클라이언트에게 응답을 보내기 위한 HttpServletResponse 객체를 생성하여 서블릿에게 전달한다. 그러면 서블릿은 받은 객체를 이용하여 content type, 응답코드, 응답 메시지등을 전송한다.

<br>

## HttpServeletRequest를 사용한 예시

``` java
@GetMapping("/getInfo")
public void getInfo(﻿HttpServletRequest request){
    log.info("RequestURL : " + request.getRequestURL() );
    log.info("RequestURI : " + request.getRequestURI() );
    log.info("QueryString : "+ request.getQueryString() );
    log.info("Get parameter" + ﻿request.getParameter("id"))
    log.info("ServerName : "+ request.getServerName() );
    log.info("ServerPort : "+ request.getServerPort() );
    log.info("Method : "+ request.getMethod() );
    log.info("Referer : "+ request.getHeader("referer") );
}
```


Q.  http://localhost:8080/getInfo?id=mangdo&year=2021로 요청을 보냈다면?

    RequestURL : http://localhost:8080/getInfo
    RequestURI : /getInfo
    QueryString : id=mangdo&year=2021
    Get parameter : mangdo
    ServerName(도메인) : localhost
    ServerPort : 8080
    Method : GET
    Referer : http://localhost:8080/getInfo 
    (Refer? 현재 요청된 페이지의 링크 이전의 웹 페이지 주소)