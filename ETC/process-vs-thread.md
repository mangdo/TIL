# 프로세스와 스레드

<br>

## 💡 프로세스
&nbsp; : 프로그램이란 실행 파일을 의미한다.  (.exe로 끝나는 파일들) <br>
&nbsp; : 프로세스란 **메모리에 올라가 실행 중인 '프로그램'** 이다.
- 메모리에 올라와 실행되고 있는 프로그램의 인스턴스(독립적인 개체)
- 운영체제로부터 시스템 자원을 할당받는 작업의 단위
- 동적인 개념

<br>


## 💡 프로세스의 특징

<img src="https://user-images.githubusercontent.com/70243735/135049732-02ffd867-e2ea-453f-a574-f226432a2df3.png" width="500px">

- 기본적으로 프로세스 당 최소 1개의 스레드를 가지고 있다.
- 프로세스는 각각 독립된 메모리 영역(Code, Data, Stack, Heap의 구조)을 할당받는다.
    - Code : 코드 자체를 구성하는 메모리 영역(프로그램 명령)
    - Data : 전역변수, 정적변수, 배열 등
    - Heap : 동적 할당 시 사용 (new(), malloc() 등)
    - Stack : 지역변수, 매개변수, 리턴 값 (임시 메모리 영역)
- 각 프로세스는 별도의 주소 공간에서 실행되며, 
한 프로세스는 **다른 프로세스의 변수나 자료구조에 접근할 수 없다.**
- 한 프로세스가 다른 프로세스의 자원에 접근하려면 프로세스 간의 통신(IPC, inter-process communication)을 사용해야 한다. (Ex. 파이프, 파일, 소켓 등을 이용한 통신 방법 이용)


<br>


## 💡 스레드(Thread)
> 프로세스 안에서 실행되는 여러 흐름의 단위 <br>
> 프로세스가 할당 받은 자원을 이용하는 실행의 단위

<img src="https://user-images.githubusercontent.com/70243735/135049909-be9c9fd4-2d60-4a22-9326-a56a892b2d72.png" width="500px">

- 스레드는 프로세스 내에서 **Code, Data, Heap 영역은 서로 공유하고 Stack 영역만 각각 할당** 받는다.
- 한 스레드가 프로세스 자원을 변경하면, 다른 이웃 스레드(sibling thread)도 그 변경 결과를 즉시 볼 수 있다.

<br>

### +) 자바 스레드(Java Thread)

- 일반 스레드와 거의 차이가 없으며, JVM가 운영체제의 역할을 한다.
- 자바에는 프로세스가 존재하지 않고 **스레드만 존재**하며, 자바 스레드는 JVM에 의해 스케줄되는 실행 단위 코드 블록이다.
- 자바에서 스레드 스케줄링은 전적으로 JVM에 의해 이루어진다.


<br>

Reference : <br>
https://magi82.github.io/process-thread/ <br>