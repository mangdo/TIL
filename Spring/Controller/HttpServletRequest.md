# HttpServletRequest

1. 웹 브라우저가 서버에 요청을 보낸다.

2. WAS가 HttpServletRequest라는 객체와 HttpServletResponse라는 객체를 생성

3. 생성된 두 개의 객체를 요청 정보에 있는 path로 매핑된 서블릿에게 전달

​

HttpServletRequest는 request 정보를 서블릿에게 전달한다.


HttpServletResponse는 WAS는 요청을 보낸 클라이언트에게 응답을 보내기 위한 HttpServletResponse 객체를 생성하여 서블릿에게 전달한다.

서블릿은 해당 객체를 이용하여 content type, 응답코드, 응답 메시지등을 전송한다.

