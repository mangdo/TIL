# 연결 리스트(Linked List)
> 연속된 메모리 위치에 저장되지 않는 선형 데이터 구조, 포인터로 연결된다.

<br>

## 💡 Linked List

**배열(array)** 은 미리 공간을 예약해놓고 그 공간에 데이터를 쓰고 읽는다.

**링크드 리스트(linked list)** 는 미리 예약을 해놓지않고 필요할때마다 데이터를 추가할 수 있는 구조다. <br>
배열은 데이터만 저장하지만, linked list는 (데이터+다음 데이터를 가르키는 주소)를 저장한다.

 

- 노드 : 데이터 저장단위(데이터값, 포인터)로 구성
- 포인터 : 각 노드안에서 다음이나 이전데이터의 주소를 가지고 있는 공간

<img src="https://user-images.githubusercontent.com/70243735/132818311-102a4c5f-c0c5-4f5e-a12c-89202b213d1a.png" width="600px">

<br>
<br>

## 💡 Linked List 장단점

### - 장점

1) 동적 크기
2) 삽입 삭제 용이하다.
3) 연속된 공간을 할당할 필요가 없다.


### - 단점

1) 저장공간의 효율이 높지않다. <br>
   -> 데이터 뿐만아니라 주소를 위한 공간이 필요하기 때문이다.<br>

2) 조회 속도가 느리다.<br>
   -> 배열은 인덱스를 통해 빠르게 접근하지만, Linked list는 연결정보를 찾는 시간이 필요하기 때문이다.<br>

3) 중간 데이터 삭제시 앞 뒤 데이터의 연결을 재구성하는 부가적인 작업이 필요하다.

<br>
<br>

## 💡 Array VS List

<img src="https://user-images.githubusercontent.com/70243735/132816924-f1835bc8-f77a-4b5d-b946-464622b7e4e6.png" width="500px">

- 배열 : 데이터의 크기가 정해져 있고, 추가적인 삽입 삭제가 일어 나지 않으며 검색을 필요로 할 때 유리.
- 리스트 : 데이터의 크기가 정해져 있지 않고, 삽입 삭제가 많이 일어나며, 검색이 적은 경우 유리.

<br>
<br>

## 💡 구현 코드 with Python

<details>
<summary> 링크드 리스트 with Python </summary>

```python
class Node:
    def __init__(self, data, next=None):
        self.data = data
        self.next = next

class NodeMgmt:
    def __init__(self, data):
        self.head = Node(data) # 맨앞 노드 생성

    # 맨끝에 노드 추가
    def add(self, data): 
        if self.head=='': # 방어 코드
            self.head = Node(data)
        else :
            node = self.head
            while node.next:
                node = node.next
            node.next = Node(data)
  
    # 전체 데이터 출력  
    def desc(self) :
        node = self.head
        while node:
            print(node.data, end=' ')
            node=node.next
      
    def delete(self, data):
        # 아무런 노드가 없다.
        if self.head =='':
            print("노드가 없습니다.")
            return
        # head 데이터 삭제
        if self.head.data == data:
            temp = self.head
            self.head = self.head.next
            del temp
        else:
            node = self.head
            while node.next:
                if node.next.data == data:
                    temp = node.next
                    node.next = node.next.next #마지막 노드였다면 null
                    del temp
                else:
                    node=node.next
            
        
#실행
linkedlist1 = NodeMgmt(0)
linkedlist1.desc() #0
print()
for data in range(1,10):
	linkedlist1.add(data)
linkedlist1.desc() #0~9까지 출력
print()
linkedlist1.delete(4)
linkedlist1.desc()#0 1 2 3 5 6 7 8 9
```
</details>





<br>
<br>
<br>

## 💡 Double Linked List
내가 원하는 데이터가 후반에 있다면 무조건 앞에서부터 검색을 하는 Linked list는 오래걸릴 수 있다. <br>
이를 보완한 double linked list는 구조가 다음과 같다.

<img src="https://user-images.githubusercontent.com/70243735/132817724-9c45b4c7-5bd3-4785-a102-3b825f740a89.png" width="500px">

<br>

## 💡 구현 코드 with Python

<details>
<summary> 더블 링크드 리스트 with Python </summary>

```python
class Node:
    def __init__(self, data, prev=None, next=None):
        self.prev = prev
        self.data = data
        self.next = next

class NodeMgmt:
    def __init__(self, data):
        self.head = Node(data)
        self.tail = self.head #처음에는 노드가 하나라서 head=tail
        
    def insert(self, data):
        if self.head == None: # 방어코드
            self.head = Node(data)
            self.tail = self.head
        else:
            node = self.head
            while node.next:
            	node = node.next
            new = Node(data)
            node.next = new
            new.prev = node
            self.tail = new
            
    def desc(self):
        node = self.head
        while node:
            print(node.data, end=' ')
            node=node.next
     
    # head부터 검색하는 코드
    def search_from_head(self, data):
        if self.head == None: #방어코드
            return False
        node = self.head
        while node:
            if node.data == data:
                return node
            else:
            	node = node.next
        return False
            
    # tail부터 검색하는 코드
    def search_from_tail(self, data):
     	
        if self.head == None:
        	return False
            
        node = self.tail
        while node:
            if node.data == data:
                return node
            else:
            	node = node.prev
        return False
     
    # 특정 숫자 앞에 데이터를 추가하는 함수
    def insert_before(self, data, before_data):
        if self.head == None: # 아예 없다면
            return False
        else:
            node = self.tail
            while node.data != before_data:
                node = node.prev
                if node == None:
                	return False
            new = Node(data)
            before_new = node.prev
            new.next = node
            new.prev = before_new
            
            node.prev = new
            before_new.next = new
            return True
        
  
# 0~9까지 넣기
double_linked_list = NodeMgmt(0)
for data in range(1,10):
  	double_linked_list.insert(data)
double_linked_list.desc()
print()

# 데이터 2앞에 1.5넣기
double_linked_list.insert_before(1.5, 2)
double_linked_list.desc()
print()

# 검색
search = double_linked_list.search_from_tail(1.5)
print(search.data)

```
</details>


<br>
<br>


출처: <br>
https://ko.wikibooks.org/wiki/%ED%8C%8C%EC%9D%BC:C_language_linked_list.png <br>
https://medium.com/@carocontrerasissa/introduction-to-linked-lists-7e948ae75d99 <br>
