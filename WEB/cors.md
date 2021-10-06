# CORS
> Cross-Origin Resource Sharing, 교차 출처 리소스 공유

<br>

## 💡 출처(Origin)

<img src="https://user-images.githubusercontent.com/70243735/136183977-9e1ad8a9-e246-4d5e-8093-9588470a40ee.png" width="500px">

&nbsp; 이때 출처는 Protolcol 과 Host 그리고 Port까지 모두 합친 것을 의미한다. URL의 구성요소 중 Protocol, Host, Port 이 세가지만 동일하면 같은 출처로 인정된다.

<br>


## 💡 SOP(Same-Origin Policy)
> “같은 출처에서만 자원을 공유할 수 있다”라는 규칙을 가진 정책

&nbsp; 브라우저는 기본적으로 동일 출처 정책(SOP)를 지켜서 다른 출처의 리소스 접근을 금지한다. 하지만 웹에서 다른 출처에 있는 리소스를 가져와서 사용하는 일은 흔한 일이다. 외부 리소스를 사용하기 위한 SOP의 예외 조항이 바로 CORS이다.

<br>

## 💡 CORS(Cross-Origin Resource Sharing)
> **다른 출처의 자원**에 접근할 수 있는 권한을 부여하도록 **브라우저**에 알려주는 정책

&nbsp; 출처를 비교하는 로직은 서버에 구현된 스펙이 아닌 브라우저에 구현된 스펙이다. 만약 CORS정책을 위반하는 요청에 서버가 정상적으로 응답을 하더라도 브라우저가 이 응답을 분석해서 CORS정책에 위반되면 그 응답은 처리하지 않게 된다.

<br>

## 💡 CORS 동작원리
### 1. Simple request
> 단순 요청 방법은 서버에게 바로 요청을 보내는 방법이다.

&nbsp; 서버에 API를 요청하고, 서버는 Access-Control-Allow-Origin 헤더를 포함한 응답을 브라우저에 보낸다. 브라우저는 Access-Control-Allow-Origin 헤더를 확인해서 CORS 동작을 수행할지 판단한다. 서버로 전달하는 요청(request)이 아래의 3가지 조건을 만족해야 서버로 전달하는 요청이 단순 요청으로 동작한다.

- 요청 메서드(method)는 GET, HEAD, POST 중 하나여야 하나.
- Accept, Accept-Language, Content-Language, Content-Type, DPR, Downlink, Save-Data, Viewport-Width, Width를 제외한 헤더를 사용하면 안 된다.
- Content-Type 헤더는 application/x-www-form-urlencoded, multipart/form-data, text/plain 중 하나를 사용해야 한다.

<img src="https://user-images.githubusercontent.com/70243735/136184287-20a0a928-ca7d-40a4-9ea5-9e80a0363e2d.png" width="600px">

<br>

### 2. Preflight Request
> 서버에 예비 요청을 보내서 안전한지 판단한 후 본 요청을 보내는 방법이다.

&nbsp; Preflight 방식은 일반적으로 웹 어플리케이션을 개발할 때 가장 마주치는 시나리오이다. 본 요청을 보내기 전에 예비 요청을 보내는데, 이 예비 요청을 Preflight라고 부르는 것이며, 이 예비 요청에는 HTTP 메소드 중 OPTIONS 메소드가 사용된다. <br>
&nbsp; Preflight 방식은 CORS를 모르는 서버를 보호하기 위한 방법이다. CORS를 모르는 서버의 경우에는 출처를 확인하지 않고 API 요청을 처리한다. 하지만 서버에서는 처리되었더라도 브라우저에서는 CORS로 에러를 발생시킨다. 이런 상황을 방지하기 위해 Preflight 방식을 사용한다.

<img src="https://user-images.githubusercontent.com/70243735/136184432-1c003616-62bb-45d6-843a-615c640ab76b.png" width="600px">


<br>
<br>
<br>


Reference : <br>

[CORS는 왜 이렇게 우리를 힘들게 하는걸까?](https://evan-moon.github.io/2020/05/21/about-cors/) <br>
[[Browser] CORS란?](https://beomy.github.io/tech/browser/cors/#simple-request) <br>