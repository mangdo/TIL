# Garbage Collection
> 힙 영역에서 사용하지 않는 메모리 영역을 찾아내서 해제하는 기능
<br>

## 💡 Garbage Collection의 수거 대상

자바의 GC는 수거 대상을 판별하기 위해 Reachability 라는 개념을 사용한다 <br>
- Reachable → 어떤 객체에 유효한 참조가 존재
- Unreachable → 어떤 객체에 유효한 참조가 존재하지 않음

<img src="https://user-images.githubusercontent.com/70243735/133929810-10a6d081-46e5-4be2-93d3-36277573143d.png" width ="500px">

<br>

## 💡 Garbage Collection 과정
> = Mark and Sweep

### Mark

GC가 GC Root로 부터 모든 변수를 스캔하면서 각각 어떤 객체를 참조하고 있는지 찾아서 마킹하는 과정이다. 즉 Reachable객체와 unReachable 객체를 식별하는 과정이다. 

### Sweep

Mark 되어있지 않은 객체들을 힙에서 제거하는 과정이다.

<br>


## 💡 stop-the-world

&nbsp; &nbsp; GC를 실행하기 위해 JVM이 애플리케이션 실행을 중지하는 것을 의미한다. 정확히는 GC를 실행하는 쓰레드를 제외한 모든 스레드들이 작업을 중단한다. GC의 종류에 따라서 stop-the-wrold를 수행하는 시간이 다르다. (Serial GC, Parallel GC, CMS GC, G1 GC 등)

<br>

### 💡 Garbage Collection이 수행되는 시점

<img src="https://user-images.githubusercontent.com/70243735/133928791-589cc641-3bc2-4200-86c6-732dd647fcf9.png" width="500px">

&nbsp; &nbsp; Garbage Collection이 일어나는 시점을 이해하기 위해서는 힙의 구조를 이해해야힌다.
힙은 Young Genration, Old Genration 그리고 Permnant Genertaion으로 이루어져 있다.
Yong은 새로운 객체들이 할당되는 영역이고 Old는 오랫동안 살아남은 객체들이 존재하는 영역이다. Permnant영역은 객체의 생명주기가 영구적일 것으로 생각하는 객체들을 관리한다. 이 영역은 GC대상에서 제외된다.<br>
&nbsp; &nbsp; GC는 Minor GC와 Major GC로 구분되는데, Minor GC는 young 영역에서, Major GC는 old 영역에서 일어난다고 정의한다. 
1. 새로운 객체가 Eden에 할당
2. Eden이 꽉 차게 되면 Minor GC가 발생한다.
3. GC(mark-sweep 과정)에서 살아남은 객체들은 Survivor 영역으로 이동한다. Survior 영역에 객체의 age가 증가한다. <br>
    : survivor 0에 객체가 있으면 survivor 1에 객체가 없어야한다.
4. 2 ~ 3과정을 반복한다.
5. 객체의 age가 특정 임계점에 도달하게 되면 Old 영역으로 이동한다.
6. Old 영역이 꽉 차게되면 Major GC가 발생한다.





<br>
<br>
<br>

출처 : <br>
https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html<br>
https://youtu.be/Fe3TVCEJhzo