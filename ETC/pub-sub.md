# Pub/Sub

## 💡 Publish Subscribe 모델
&nbsp; : 비동기 메시징 패러다임이다. <br>
&nbsp; : Pub-Sub 모델에서 publishers의 메시지는 메시지 마다 수신자가 정해지는 개념이 아닌, 메시지를 정해진 클래스대로 구분하고, 각 클래스를 구독한 모든 subscribers에게 전달된다. publishers와 subscribers는 서로에 대한 지식이 없어도 원하는 메시지만을 전달할 수 있다. 이러한 디커플링은 더 다이나믹한 네트워크 토폴리지와 높은 확장성을 가능하게 한다.
<br>

## 💡 Pub/Sub vs Message queue

<img width="502" alt="스크린샷 2022-11-06 오후 7 37 42" src="https://user-images.githubusercontent.com/70243735/200166043-db798cce-dcd5-4612-89f8-673d889d5fe7.png">


&nbsp; : 메시지 큐는 하나의 메시지를 한명의 subscribe가 소비할 수 있다. subscriberA가 메시지1을 소비했다면, 이 메시지를 subscriberB가 또 소비할 수는 없다. 그럴러면 큐를 하나 더 만들어야한다.  <br>
&nbsp; : 위의 Message Queue model의 그림은 고객이 3개의 제품을 구매한 이벤트가 발생했고, 이를 Inventory 알리는 큐와 Order에 알리는 큐, 총 두개가 필요하다. <br>
&nbsp; : 하지만 Pub/Sub 구조에서는 하나의 메시지를 여러명이 소비할 수 있다. <br> 
&nbsp; : 또한 발생한 이벤트를 보게되면, 미묘하게 다른 것을 알 수 있다. 큐 모델에서는 setInventory(300)라고 했지만 Pub/Sub에서는 5번 상품을 구매한 이벤트라고 하고 있다. 큐 모델의 이벤트의 경우는 Subscriber이 수행해야할 작업, 해야할 결과를 알려주고 있지만, Pub/Sub에서는 실제로 발생한 이벤트의 세부정보에 집중하고 있다. 또한 큐 모델의 이벤트는 상태 결과를 지정하는 setInventory(300)이기 때문에 setInventory(100), setInventory(500) 이벤트와 섞인다면, 의도했던 결과와 달라질 수 있기때문에 이벤트 순서를 꼭 보장해야한다. 

<br>

## 💡 Pub/Sub 필터링 vs 팬아웃 기법

&nbsp; : 이벤트 스트림에 모든 Subscriber가 필요하거나 필요하지 않은 데이터가 포함될 수 있기때문에 지정된 Subscriber가 수신하는 데이터를 제한해야할 경우가 자주있다. 이럴때 사용할 수 있는 기법이 이벤트 필터링과 이벤트 팬아웃이다.


<img width="495" alt="스크린샷 2022-11-06 오후 7 39 00" src="https://user-images.githubusercontent.com/70243735/200166094-f60a446b-f748-46ae-9f74-504457a094fa.png">

<img width="495" alt="스크린샷 2022-11-06 오후 7 39 21" src="https://user-images.githubusercontent.com/70243735/200166109-899e7ced-ec41-44cd-a2cc-daf9589d2893.png">


&nbsp; : Subscriber이 각 메시지를 읽고 적용 가능한지 확인하는 대신, 메시징 시스템의 필터링 논리가 메시지를 평가하고 다른 Subscriber가 접근하지 못하도록 제한한다. 이에 반해 이벤트 팬아웃 메커니즘은 해당 Subscriber 하위 집합에 관련된 topic에 따라 메시지를 다시 게시한다.

<br>

## 💡 GCP Pub/Sub 기본 아키텍처
&nbsp; : Pub/Sub은 크게 Control Plane과 Data Plane으로 구분된다. <br> 
&nbsp; : Data Plane은 Publisher와 Subscriber간의 데이터 이동을 처리하고, Control Plane은 Publisher와 Subscriber를 Data Plane의 서버에 할당하는 작업을 처리한다. Data Plane의 서버를 Forwarder라고 하고, Control Plane의 서버를 Router라고 한다. Publisher와 Subscriber가 자신에게 할당된 Forwarder에  접근할 수 있는 한, Router로부터 정보를 받을 필요가 없다. 따라서 기존에 연결된 클라이언트에 영향을 주거나 메시지를 송수신하지 않고도 Pub/Sub Control plane을 업데이트 할 수 있다.

<br>

### 💡 GCP Pub/Sub Control Plane
&nbsp; : 클라이언트는 Router가 권장하는 Forwarder와의 연결을 선호하지만, 여러번 실패하는 경우 다른 데이터 센터에 있는 Forwarder와의 연결을 시도한다. Pub/Sub 클라이언트에 대해 이러한 구현 세부정보를 추상화하기 위해 클라이언트와 클리언트를 대신하여 이 연결 최적화를 수행하는 Forwarder 사이에 서비스 프록시가 있다.

<br>

### 💡 GCP Pub/Sub Data Plane - The Life of a Message
&nbsp; : Data Plane을 더 잘 이해하기 위해서 메시지의 라이프를 알아보자. 일반적으로 메시지는 다음과 같은 단계를 거친다.
1. Publisher가 메시지를 전송한다.
   - 이 메시지는 프록시 레이어로 암호화되어 Publisher와 연결된 Forwarder인 Publishing Forwarder로 전송된다.
2. 메시지를 스토리지에 저장한다.
   - Publishing Forwarder로 전달된 메시지는 즉시 스토리지에 저장된다. 
3. Pub/Sub이 메시지 수신 확인을 Publisher에게 전달하고 연결된 모든 구독에 대한 메시지 전송을 보장한다.
   - Forwrder는 메시지를 먼저 클러스터 N개에 기록하며, N/2이상의 클러스터에 저장되면 메시지는 지속되는 것으로 간주한다. 메시지가 지속되면 Publishing Forwarder는 메시지 수신확인을 Publisher에게 전송하며, 이때 Pub/Sub은 연결된 모든 구독에 메시지를 전달할 것을 보장한다.
4. 메시지를 스토리지에 저장함과 동시에, Pub/Sub이 이를 Subscriber에게 전달한다.
    - Subscriber은 Subscribing Forwarder과의 연결을 통해서 메시지를 가져옵니다. Subscribing Forwarder는 Subscriber에서부터 Publisher로 메시지를 전달하는 역할을 한다. Pull Subscriber에게 "연결"이라 함은 Pull Request 요청을 실행함을 의미하며, Push Subscriber에게 "연결"이라 함은 Push endpoint를 Pub/Sub에 등록하는 것을 의미한다. 구독이 생성되면 모든 메시지는 해당 구독으로 전달되도록 보장되며 이를 "sync-point guarantee"라고 한다.
    - 각 subscribing forwarder는 토픽에 대한 메시지 원본이 있는 publishing forwarder에게 메세지를 요청해야한다. publishing forwarder는 확인하지 않은 메시지를 subscribing forwarder에게 전송하며, 이후 해당 메시지는 subscriber에게 전달된다.
5. Subscriber가 메시지 처리 확인을 Pub/Sub에 전송한다.
    - 메시지를 처리하면 subscriber는 subscribing forwarder에게 확인을 전송한다. subscribing forwarder는 publishing forwarder에게로 이를 전달하며, publishing forwarder는 이 확인을 publish message 원본에 저장한다.
6. 각 토픽에 대해 하나 이상의 구독자가 메시지를 확인하면 Pub/Sub이 메시지를 스토리지에서 삭제한다.


<br>

## 💡 GCP Pub/Sub의 subscription type

### Pull subscription
&nbsp; : Pull 구독의 경우, subscriber client가 Pub/Sub 서버에 요청하여 메시지를 가져온다. REST Pull API, the RPC PullRequest API, the REST StreamingPullRequest API, the RPC StreamingPullRequest API를 사용할 수 있다. 대부분의 subscriber client는 이러한 요청을 직접 수행하기보다는 Google Cloud 가 제공하는 라이브러리를 이용하여 스트리밍 pull requests을 내부적으로 수행하고 메시지를 비동기식으로 전송한다. 

<img width="490" alt="스크린샷 2022-11-06 오후 7 43 33" src="https://user-images.githubusercontent.com/70243735/200166274-f6ba01ce-350c-42ac-9fcb-4149832ac07d.png">


1. subscriber 클라이언트는 pull 메서드를 명시적으로 호출하여 메시지 전달을 요청한다. 이는 위의 이미지 속의 "PullRequest"과정이다.
2. Pub/Sub 서버는 0개 이상의 메시지와 acknowledgment ID로 응답한다. 이는 위의 이미지 속의 "PullResponse"과정이다.
3. subscriber 클라이언트가 acknowledged 메서드를 명시적으로 호출한다. 클라이언트는 반환된 acknowledgment ID를 사용하여 해당 메시지가 처리되었으며 다시 전달할 필요가 없음을 확인해준다. 이는 이미지 속의 "AckRequest"과정이다.

<br>

### Push subscription
&nbsp; : Push 구독의 경우, Pub/Sub 서버는 subscriber client에 메시지 전송을 요청한다.

<img width="498" alt="스크린샷 2022-11-06 오후 7 43 38" src="https://user-images.githubusercontent.com/70243735/200166265-7a49b854-3483-4350-a8b6-76a374af8faa.png">

1. Pub/Sub 서버는 각 메시지를 미리 구성된 엔드포인트에 있는 subscriber 클라이언트에 하나의 HTTPS 요청으로 전송한다.
2. 엔드포인트가 HTTP 성공상태 코드를 반환하여 메시지를 확인한다.
3. Pub/Sub는 성공응답을 수신하는 속도에 따라 푸시 요청의 비율을 동적으로 조정한다.

<br>

### Decide on your subscription type

<figure>
    <table>
        <thead>
            <tr>
                <th> </th>
                <th>Push</th>
                <th>Pull</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Use case</td>
                <td>
                    - 대량 메시지 (초당 GB) <br>
                    - 메시지 처리 효율성과 처리량이 중요한 경우 <br>
                    - 공개된 HTTPS 엔드포인트를 설정할 수 없는 황경
                </td>
                <td>
                    - 여러 토픽을 같은 웹훅으로 처리해야하는 경우 <br>
                    - App Engine Standard, Cloud Functions subscribers
                </td>
            </tr>
            <tr>
                <td>Flow control</td>
                <td>Subscriber client가 전달속도를 조절할 수 있다. </td>
                <td>
                    - Pub/Sub 서버가 자동으로 흐름 제어를 구현한다. <br>
                    - 클라이언트측에서 메시지 흐름을 처리할 필요는 없지만, HTTP 오류를 돌려보내서 클라이언트가 현재 메시지 부하를 처리할 수 없을 표시할 수 있다.
                </td>
            </tr>
            <tr>
                <td>효율성 및 처리량</td>
                <td>일괄전달과 확인 및 대량의 동시소비가 가능해서 낮은 CPU에서도 높은 처리량을 구현할 수 있다. 메시지 전송 시간 최소화를 위해 적극적인 폴링을 사용하면 효율성이 떨어질 수 있다. </td>
                <td>
                    요청당 메시지 1개를 전달하며 대기 메시지 최대 숫자를 제한 한다.
                </td>
            </tr>
        </tbody>
    </table>
</figure>

<br>




## Reference
[Event-driven architecture with Pub/Sub](https://cloud.google.com/solutions/event-driven-architecture-pubsub)
<br>
[Pub/Sub: A Google-Scale Messaging Service](https://cloud.google.com/pubsub/architecture)
<br>
[Pub/Sub: Choose a subscription type](https://cloud.google.com/pubsub/docs/subscriber)

