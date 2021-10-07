# Spring MVC
> Model, View, Controller를 분리한 디자인 패턴

<br>

## 💡 Spring MVC

: MVC 패턴의 주된 목적은 **Business logic과 Presentation logic을 분리할 수 있다는 것이다.** <br>
: 각자의 책임을 나눠서 명확하게 해줄 수 있다. <br>
- Model은 데이터 관리와 비지니스 로직을 처리하는 부분이다.
- View 는 '사용자에게 보여질 페이지' 를 담당한다
- Controller 는 '사용자의 요청을 받고, 응답을 주는 로직'을 담당한다.

<br>

## 💡 Spring MVC 동작 과정

<img src="https://user-images.githubusercontent.com/70243735/136377320-96e5960b-f3f9-4c19-8453-4e2ba7b77294.png" width="500px">


1. 클라이언트가 url을 요청하면, 웹 브라우저에서 스프링으로 request가 보내진다.
2. `Handler Mapping`을 통해 해당 url을 담당하는 Controller를 탐색 후 찾아낸다.
3. 찾아낸 `Controller`로 request를 보낸다.
4. Controller는 Business Logic을 처리하고 view에 전달할 model을 구성한다.
5.  `View Resolver`를 통해 Controller가 리턴한 View name을 기반으로 적절한 View를 찾아준다.
6. 받아낸 View 페이지 파일에 Model을 보낸 후, 클라이언트에게 보낼 페이지를 완성시켜 받아낸다.
7. 완성된 View 파일을 클라이언트에 response하여 화면에 출력한다.

<br>
<br>


<img src="https://user-images.githubusercontent.com/70243735/136377407-b133f506-9102-4e2d-9596-1b4139972964.png" width="600px">

<br>
<br>

Reference :

[https://velog.io/@miscaminos/Spring-MVC-framework](https://velog.io/@miscaminos/Spring-MVC-framework)