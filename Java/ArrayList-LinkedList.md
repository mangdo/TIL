# Array List vs Linked List

List 인터페이스를 구현한 대표적인 클래스들은 다음과 같다.
1. ArrayList<E>
2. LinkedList<E>
3. Vector<E> <br>
    : 기존 코드와의 호환성을 위해서만 남아있으며 현재는 거의 사용하지 않는다.

<br>

<img src="https://user-images.githubusercontent.com/70243735/133979418-72317669-0988-417c-9bb9-3d9e431f6f90.png" width="500px">


## 💡 ArrayList
> ArrayList는 내부적으로 **배열**을 이용하여 요소를 저장한다.

#### 장점
- 인덱스를 이용해 조회 속도가 빠르다

#### 단점
- 추가, 삭제 속도가 느리다<br>
    : 배열의 크기를 늘리기 위해서는 새로운 배열을 생성하고 기존의 요소들을 옮겨야 하는 복잡한 과정을 거쳐야 한다.<br>
    : 이 과정은 자동으로 수행되지만, 상황마다 적절한 자료구조를 선택해야 하기 때문에 알고 있어야 한다!!

#### 사용 방법
```java
ArrayList<Integer> arrList = new ArrayList<Integer>();

// 요소의 저장
arrList.add(10);
arrList.add(20);

// 요소의 제거, 1번 인덱스 요소 삭제
arrList.remove(1);

// set() 메소드를 이용한 요소의 변경
arrList.set(0, 100);

// for 문과 get() 메소드를 이용한 요소의 출력
for (int i = 0; i < arrList.size(); i++) {
    System.out.print(arrList.get(i) + " ");
}
```

<br>
<br>

## 💡 LinkedList
> LinkedList는 내부적으로 이중 연결 리스트(doubly linked list)를 구현하여 요소를 저장한다. <br>

: 배열(Array)은 요소들이 순차적으로 저장된다. <br>
&nbsp; 하지만 연결 리스트(LinkedList)는 요소들이 **비순차적**으로 저장되며, 이러한 요소들 사이를 포인터로 연결하여 구성한다.

#### 장점
- 삽입, 삭제 속도가 빠르다 <br>
    : 양방향 포인터 구조로 데이터의 삽입, 삭제 시 해당 노드의 주소지만 바꾸면 되기 때문이다.

#### 단점
- 조회 속도가 느리다. <br>
    : 데이터의 조회 시 처음부터 노드를 순회해야 하기 때문이다.


#### 사용 방법
: ArrayList와 동일한 List 인터페이스를 사용하기 때문에 사용 방법이 거의 동일하다.

```java

    LinkedList<Integer> arrList = new LinkedList<Integer>();

        // 요소의 저장
        arrList.add(10);
        arrList.add(20);

        // 요소의 제거, 1번 인덱스 요소 삭제
        arrList.remove(1);

        // set() 메소드를 이용한 요소의 변경
        arrList.set(0, 100);

        // for 문과 get() 메소드를 이용한 요소의 출력
        for (int i = 0; i < arrList.size(); i++) {
            System.out.print(arrList.get(i) + " ");
        }

```


<br>
<br>
<br>


출처:

[http://tcpschool.com/java/java_collectionFramework_list](http://tcpschool.com/java/java_collectionFramework_list)   
[https://devlog-wjdrbs96.tistory.com/64](https://devlog-wjdrbs96.tistory.com/64)