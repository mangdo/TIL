# REST API
> 자원의 위치는 HTTP URI로, 자원에 대한 행위는 HTTP Method로 API를 설계하는 방식이다.

<br>


## 💡 REST API에 대한 나의 생각

REST API의 정확한 의미, 학술적 의미를 알고 싶다면 다음 영상을 참고해주세요. <br>
[Day1, 2-2. 그런 REST API로 괜찮은가](https://youtu.be/RP_f5dMoHFc) <br>

REST는 자원의 효과적으로 전달할 수 있는 방법입니다. <br>
그래서 REST API는 자원의 위치는 HTTP URI로, 자원에 대한 행위는 HTTP Method로 API를 설계하는 방식입니다. <br>
제가 실제로 최대한 REST스럽게 API를 설계하면서 느낀 최대 장점은 (HTTP를 최대한 활용해서) **이해하기 쉽고 관리하기 쉬운 API**를 만들 수 있다는 점이었습니다. 

<br>

## 💡 REST API 구성 요소

1. **자원** (Resource) <br>
    : HTTP URI
2. **자원에 대한 행위** (Verb) <br>
    : HTTP Method
3. **자원에 대한 표현** (Representations) <br>
    : REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타내어 질 수 있다.
    : JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.

<br>

## 💡 REST API 설계 규칙

1. URI는 정보의 자원을 표현해야 한다.
    - resource는 동사보다는 **명사**를 사용한다.
    - resource는 영어 소문자 **복수형**을 사용하여 표현한다.
    - Ex) `GET /Member/1` -> `GET /members/1`
2. 자원에 대한 행위는 HTTP Method(GET, PUT, POST, DELETE 등)로 표현한다.
    - URI에 행위에 대한 동사 표현이 들어가면 안된다.
    - Ex) `GET /members/insert/2` -> `POST /members/2`
3. 슬래시 구분자(/ )는 계층 관계를 나타내는데 사용한다.
    - Ex) `http://restapi.example.com/houses/apartments`
4. URI 마지막 문자로 슬래시(/ )를 포함하지 않는다.
    - REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.
    - Ex) `http://restapi.example.com/houses/apartments/ (X)`
5. 하이픈(- )은 URI 가독성을 높이는데 사용
    - 불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높인다.
6. 밑줄(_ )은 URI에 사용하지 않는다.
    - 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 하므로 가독성을 위해 밑줄은 사용하지 않는다.
7. URI 경로에는 소문자가 적합하다.
    - URI 경로에 대문자 사용은 피하도록 한다.
    - RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문이다.
8. 파일확장자는 URI에 포함하지 않는다.
    - REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다.
    - Accept header를 사용한다.
    - Ex) `http://restapi.example.com/members/soccer/345/photo.jpg (X)`
    - Ex) `GET / members/soccer/345/photo HTTP/1.1 
    Host: restapi.example.com 
    Accept: image/jpg (O)`

<br>

## 💡 REST 특징

1. Server-Client(서버-클라이언트 구조)
2. Stateless(무상태)
3. Cacheable(캐시 처리 가능)
4. Layered System(계층화)
5. Code-On-Demand(optional)
6. Uniform Interface(인터페이스 일관성)


<br>
<br>

출처:

[https://meetup.toast.com/posts/92](https://meetup.toast.com/posts/92)

[https://ko.wikipedia.org/wiki/REST](https://ko.wikipedia.org/wiki/REST)
[https://doorisopen.github.io/developers-library/Web/2020-06-04-web-rest-api-guide](https://doorisopen.github.io/developers-library/Web/2020-06-04-web-rest-api-guide)
[https://github.com/WeareSoft/tech-interview/blob/master/contents/network.md#rest와-restful의-개념](https://github.com/WeareSoft/tech-interview/blob/master/contents/network.md#rest%EC%99%80-restful%EC%9D%98-%EA%B0%9C%EB%85%90)

