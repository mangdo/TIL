# HTTP method
> 주어진 리소스에 수행하길 원하는 행동, 서버가 수행해야 할 동작을 나타낸다.

<br>

## 💡 주요 HTTP method 종류

- **GET** <br>
    : 리소스의 조회에 사용한다.<br>
- **POST** <br>
    : 메시지 바디를 통해 서버로 요청 데이터를 전달한다.<br>
    : 주로 새로운 리소스를 등록할 때 사용한다.<br>
- **DELETE** <br>
    : 목적 리소스의 삭제 요청하는 데 사용한다.<br>
- **PUT** <br>
    : 목적 리소스를 현재 요청 데이터로 전부 수정한다.<br>
    : PUT은 POST와 다르게 클라이언트가 **리소스의 위치**를 알고 URI를 지정해 주어야 한다!<br>
    ex) PUT /members/100<br>
- **PATCH** <br>
    : 목적 리소스를 **부분적으로 변경**한다. <br>
    : 지원하지 않는 경우도 있어 이런 경우 PUT이나 POST로 대체하여 사용한다. <br>

<br>

## 💡 기타 HTTP method 종류

- HEAD : GET과 동일하지만 메시지 바디를 제외하고 반환
- OPTIONS : 대상 리소스에 대한 통신을 설정하는 데 사용
- CONNECT : 대상 자원으로 식별되는 서버에 대한 터널을 설정
- TRACE : 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

<br>


## 💡 HTTP method 속성

1. 안전(Safe Methods)

    : 서버의 리소스를 변경하지 않는다는 의미이다.

2. 멱등성(Idempotent Methods) ⭐

    : 메서드를 계속 호출해도 결과가 똑같다는 의미이다. 
    : 모든 안전한 메서드는 멱등성 또한 갖지만, 모든 멱등성을 지닌 메서드가 안전한 것은 아니다. 
    : 예를 들어 PUT과 DELETE는 둘 다 멱등성을 가졌지만 안전하지는 않은 메서드다.

3. 캐시 가능(Cacheable Methods)

    : 캐싱을 해서 데이터를 효율적으로 가져올 수 있다는 뜻이다. 
    : GET, HEAD, POST, PATCH가 캐시가 가능하지만 실제로는 GET과 HEAD만 주로 캐싱이 쓰인다고 한다.


    <img src="https://user-images.githubusercontent.com/70243735/134891746-534f2b2b-2451-4bd2-8ea8-35a7e8273c16.png" width="500px">


<br>

Reference : <br>
[https://developer.mozilla.org/ko/docs/Web/HTTP/Methods](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods) <br>
[https://ko.wikipedia.org/wiki/HTTP#메시지_포맷](https://ko.wikipedia.org/wiki/HTTP#%EB%A9%94%EC%8B%9C%EC%A7%80_%ED%8F%AC%EB%A7%B7)