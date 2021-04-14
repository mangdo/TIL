# Internet vs Web

*Internet이 제공하는 서비스 중 하나인 Web*

<br>
<br>


# **[ Internet ]**

> 인터넷 프로토콜(TCP/IP)를 기반으로 전 세계적으로 연결된 컴퓨터 네트워크    

&nbsp; 1960년, 미국 내에서 중요 군사정보를 어떻게 관리 할지에 대해서 고민했었다.   
&nbsp; 처음에는 철벽 요새를 두어 모든 정보를 중앙 집중형으로 관리하고자 했으나, 그 요새가 핵공격을 당하게 된다면 치명적인 결과를 불러일으킬 수 있었다. 그래서 여러 곳에 서버를 분산 설치한 후, 이를 서로 연결하여 일부 서버가 공격당하더라도 나머지 서버들로 관리하는 방안을 선택하였다.    
&nbsp; 그 결과가 바로 <u>최초의 패킷 스위칭 네트워크</u>인 **ARPAnet**이다.
<br>

<img src="https://user-images.githubusercontent.com/70243735/114553907-191e0e80-9ca1-11eb-82b7-a9133454d8b9.png" width ="550px">

&nbsp; 본래 군사목적이였던 아파넷을 기업과 대학에서 쓰고자 하는 요구가 늘어났다. 이에 미국 국방부는 군사용 네트워크(MILNET)와 민간용 네트워크(ARPAnet)을 분리시켰다. 또한 초창기에 사용하던 NCP(Network Control Program)보다 네이버 속도 및 안정성이 향상된 **TCP/IP를 공식 프로토콜**로 도입했다.

&nbsp; ARPANET과 별도로 1986년 미국과학재단은 5곳의 슈퍼컴퓨터 센터를 연결하여 NSFnet을 만들었는데, 1980년대 말에 이르러 ARPANET이 흡수통합되면서 대학, 연구소, 정부기관, 기업 등 세계 모든 곳을 연결하는 국제 통신망으로 발전하게 되었다. NSFnet의 등장은 네트워크 기술이 정부나 공공기관 중심이 아닌 민간에까지 확대되는 결과를 가져왔다.   
&nbsp; 이로 인해 인터넷 컴퓨터 네트워크의 기본 구조가 갖춰졌으며, 이 때를 즈음하여 'Internet'은 단순히 일반명사 'InterNetwork'의 약어가 아닌 고유명사 취급을 받기 시작했다.

 
&nbsp; 인터넷이란 이름은 1973년 TCP/IP를 정립한 빕튼 서프와 밥 간이 '**네트워크의 네트워크**'를 구현하여 **모든 컴퓨터를 하나의 통신망 안에 연결**(InterNetwork)하고자 하는 의도에서 이를 줄여 인터넷(Internet)이라고 처음 명명하였던 데 어원을 두고 있다. 


<br>

# **[ WEB의 출현 ]**
> 1990년, 웹의 출현으로 인터넷은 큰 변화를 겪게 된다.

&nbsp; 최초의 웹페이지, http://info.cern.ch
<img src="https://user-images.githubusercontent.com/70243735/114554745-048e4600-9ca2-11eb-8890-61bc8739d042.png" width="550px">

&nbsp; 유럽입자물리연수소의 소프트웨어 공학자, 팀 버너스리는 전 세계의 대학 및 연구소들끼리의 상호 연구를 위해 정보를 신속하게 교환할 수 있도록 해야 한다고 판단하였다. 문서뿐만 아니라 소리, 동영상 등을 망라하는 데이터베이스를 구축하고 이를 전문 열람 소프트웨어로 열람하는 방식을 생각해 내게 된다. 이것이 World Wide Web(줄여서 WEB)의 탄생 배경이다.

```
1990.10 
 인터넷을 이용해서 웹페이지를 만드는 편집기를 만든다.
1990.11
 최초의 웹 브라우저인 World Wide Web이라는 프로그램을 만든다.
1990.12
 웹서버라는 프로그램을 만든다.
 이 웹서버가설치되어있는 컴퓨터에 info.cern.ch라는 주소를 부여한다.
```

<br>

# **[ WEB ]**
> 인터넷에 연결된 컴퓨터가 서로 정보를 주고 받는 전세계적인 정보 공간

<img src="https://user-images.githubusercontent.com/70243735/114555234-76668f80-9ca2-11eb-9bf6-cd512084b586.png" width="450px">

&nbsp; 사람들이 웹을 통해 정보자원에 접근하여 이용할 수 있는 것은 다음과 같은 메커니즘을 갖고 있기 때문인데 이것을 **웹의 3대 요소**라고 부른다.

* HTTP (**H**yperText **T**ransfer **P**rotocol)   
    : 웹 클라이언트와 웹 서버가 정보를 주고 받을 때 사용하는 통신 규약
    : HTTP를 통해 전달되는 자료는 http:로 시작하는 URL로 조회할 수 있다

* URL (**U**niform **R**esource **L**ocator)   
    : 네트워크상 정보 자원의 위치를 표시하기 위한 표기법

* HTML(**H**yper**T**ext **M**arkup **L**anguage)   
    : 웹페이지를 위한 마크업 언어   
    : 링크를 통해 자원들 사이를 쉽게 항해 할 수 있는 언어

<br>

<img src="https://user-images.githubusercontent.com/70243735/114555772-fee53000-9ca2-11eb-98f2-9bed0ec9bcf3.png" width="450px">

웹은 인터넷이 포함하고 있는 서비스 중 하나이다. 다음은 인터넷이 제공하고 있는 서비스들 중 일부이다.

 이름|프로토콜|포트|기능
 -|-|-|-|
Web	  |HTTP| 80| 웹 서비스
Email |SMTP/POP3/IMAP| 25/110/114| 전자 메일 서비스
FTP	  |FTP|	21|	파일 전송 서비스
DNS	  |DNS|	23|	네임 서비스
NEWS  |NNTP| 119|인터넷 뉴스 서비스
Telnet|Telnet|	23|	원격 터미널 접속
 

<br>

# **[ WEB의 동작 방식 ]**
> web client(web brower)가 정보를 요청하고 web server는 정보를 응답한다.

<img src ="https://user-images.githubusercontent.com/70243735/114715490-13dac580-9d6e-11eb-8ee9-6a34d08ca415.png" width="450px">

1. 두대의 컴퓨터는 모두 인터넷으로 연결되어 있다.

2. 하나의 컴퓨터에는 web brower를, 다른 하나의 컴퓨터에는 web server라는 프로그램을 설치한다.

3. 웹서버가 깔려있는 컴퓨터는 198.168.0.13라는 IP주소를 가지고 있다.

    웹서버가 설치되어있는 컴퓨터의 하드디스크에
    어느 디렉토리안에 index.html이 저장되어있다.

4. 웹 브라우저에서 주소창에 http://198.168.0.13/index.html 을 입력한다.

    웹 브라우저는 인터넷을 통해 198.168.0.13에 해당하는 컴퓨터에 "index.html을 원한다"는 요청을 보낸다.

5. 198.168.0.13에 해당하는 컴퓨터에 설치된 web server라는 프로그램이 하드디스크에서 index.html을 찾아 응답한다.

6. 웹 브라우저는 index.html 파일의 내용(코드)를 읽어서 화면에 표시한다.


이렇게 web Brower가 설치되어있는 컴퓨터와 web Server가 설치되어있는 컴퓨터가 서로 정보를 주고 받는다. 이때 웹 브라우저가 웹서버에 요청하기 위해서는 웹서버의 IP주소(Internet Protocol address)가 필요하다.

 

 
<br>
<br>
 

참고 출처 :

youtu.be/pYOEy_mAMpI   
https://namu.wiki/w/%EC%9D%B8%ED%84%B0%EB%84%B7   
victorydntmd.tistory.com/285    
ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%84%B7   
www.slideshare.net/ChulgyuShin/ss-12524684