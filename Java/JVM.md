# JVM
> Java Virtual Machine(자바 가상 머신)은 자바 바이트코드를 실행할 수 있는 소프트웨어다.

<br>

## 💡 JVM이란?
&nbsp; &nbsp; Java Virtual Machine(자바 가상 머신)의 약자이다. 가상 머신이란, 프로그램을 실행하기 위해서 물리적 머신과 유사한 머신을 소프트웨어로 구현한 것이다. JVM의 역할은 대표적으로 다음 두가지다.

1. 자바 프로그램이 어떤 운영체제 위에서도 실행될 수 있도록 한다.<br>

<img src="https://user-images.githubusercontent.com/70243735/133730262-47a52cc0-f069-4631-a4ec-c71b28b61a03.png" width="400px">


JVM은 자바의 "*Write Once, Run Anywhere*" 을 가능하게 한다.   
자바가 나오기 전, C언어는 운영체제에 맞게 프로그램을 수정해야 했다.
하지만 자바의 경우 JVM이 자바와 운영체제 사이에 위치하여 중개자 역할을 하면서 프로그램을 수정하지 않고도 여러 운영체제에서 사용 가능하다.


2. 프로그램 메모리를 관리하고 최적화한다.

<br>

## 💡 Java의 실행 과정


1. 프로그램이 실행되면 JVM은 **OS로부터** 이 프로그램이 필요로하는 **메모리를 할당**받는다. <br>
   JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리한다.

2. **자바 컴파일러**(javac)가 자바 소스코드를 읽고, 자바 바이트코드(.class)로 변환한다.

3. **Class Loader**를 통해 class 파일들을 JVM 메모리 영역으로 로딩한다.

4. 로딩된 class파일들은 **Execution engine**을 통해 해석된다.

5. 해석된 바이트 코드는 **메모리 영역에 배치되어 실질적인 수행**이 이루어진다. <br>
   이러한 실행 과정 속 JVM은 필요에 따라 스레드 동기화나 가비지 컬렉션 같은 메모리 관리 작업을 수행한다.

<br>

## 💡 JVM의 구조

<img src="https://user-images.githubusercontent.com/70243735/133784882-2b7ed7bc-2662-4259-add8-194eb64f5eba.png" width="500px">

### 1) Class Loader
: 런타임 시에 동적으로 JVM 내로 클래스파일을 로드하고, 메모리에 배치시킨다.


### 2) Runtime Data Areas
: JVM이 프로그램을 수행하기 위해 OS에서 할당받은 메모리 공간 <br>
: Method Area, Heap 영역은 모든 스레드가 공유하고 나머지 공간들은 스레드 마다 하나씩 생성된다.

- Method Area <br>
 : class area, static area라고도 불린다. <br>
 : JVM이 읽은 각각의 클래스와 인터페이스에 대한 클래스 멤버 변수, 메소드 정보, Type 정보 들이 저장되는 공간이다.

- heap 영역 <br>
 : 동적으로 생성된 데이터가 저장되는 영역으로, GC의 대상이 되는 공간이다.

- stack 열역 <br>
 : 지역변수, 매개변수, 메서드 정보, 임시 데이터 등을 저장하는 공간이다.

- PC Register <br>
 : 스레드가 어떤 부분을 어떤 명령어로 실행할지를 저장하는 공간이다. <br>
 : 스레드가 시작될 때 생성되며, 현재 수행 중인 JVM의 명령어 주소를 저장한다.

- Native Method stack <br>
 : Java가 아닌 다른 언어로 작성된 코드(c, c++)를 위한 공간이다.


### 3) Excution Engine
: Runtime Data Area에 로드된 클래스파일의 바이트코드를 실행하는 엔진이다. <br>
: 바이트코드를 실행시키기 위해서 바이트코드를 기계어로 바꾸는 작업이 필요한데, 여기서 두 가지의 방법이 있다. <br>
1) Interpreter  -> 명령어를 한 줄 한 줄 해석해서 실행한다. <br>
2) JIT (Just-In-Time) compiler -> 자바 컴파일러가 생성한 자바 바이트 코드를 런타임에 바로 기계어로 변환해주는 컴파일러이다. <br>

+) 가비지 컬렉터 -> 힙 영역에서 사용되지 않는 객체들을 제거한다.


### 4)  JNI(Java Native Interface)
 : 자바 애플리케이션에서 C, C++, 어셈블리어로 작성된 함수를 사용할 수 있는 방법을 제공해준다.

### 5) Native Method Library
 : C, C++로 작성된 라이브러리 이다.


<br>
<br>
<br>
<br>

출처 :

https://www.scientecheasy.com/2021/03/what-is-jvm.html/   
https://asfirstalways.tistory.com/158
https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=rokey_89&logNo=221658053244