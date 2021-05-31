# Disjoint Sets(서로소 집합)

<br>

## 💡 Disjoint Sets(서로소 집합)
<img src="https://user-images.githubusercontent.com/70243735/120186181-1fb31600-c24e-11eb-9cf2-0f84c1a94497.png" width="500px">

&nbsp; 서로소 집합이란, 공통 원소가 없는 두집합을 의미한다. 왼쪽 그림에서 집합 A와 B는 서로소 관계이고, 오른쪽 그림에서  집합 A와 B는 서로소 관계가 아니다.

&nbsp; 서로소 집합 자료구조는 서로소 부분 집합들로 나누어진 원소들의 데이터를 처리하기 위한 자료구조이다. 서로소 집합 자료구조는 **union-find 자료구조**라고도 불린다. 사용되는 연산의 이름 자체가 union과 find이기도 하고, 두 집합이 서로소 관계인지 확인할 수 있다는 말은 각 집합이 어떤 원소를 공통으로 가지고 있는지를 확인할 수 있다는 말과 같기 때문이다.

<br>

## 💡 Disjoint Sets 동작 과정
&nbsp; Disjoint Sets 를 구현할 때는 트리 자료구조를 이용하여 집합을 표현한다. **트리**로 부분집합을 표현하고 **find**를 통해 루트 노드를 찾고 **union**으로 트리를 합친다. 서로소 집합 계산 알고리즘은 다음과 같다.

1. union(합집합)연산을 확인하여, 서로 연결된 두 노드 A, B를 확인한다.

    (1) A와 B의 **루트노드 A'와 B'** 를 각각 찾는다.

    (2) **A'를 B'의 부모노드로 설정**한다.(=B'가 A'를 가리키도록 한다.)

    &nbsp; &nbsp; : *보통 A'와 B'중에서 더 번호 작은 원소가 부모 노드가 되도록 구현한다.*

2. 모든 union(합집합) 연산을 처리할 때까지 1번 과정을 반복한다.

<br>

예시로 다음과 같은 union연산을 주어졌을 때 동작과정을 살펴보겠다.

    union(1, 4) union(2, 3) union(2, 4) union(5, 6)
 

**[ 초기 단계 ]**

<img src="https://user-images.githubusercontent.com/70243735/120187532-de236a80-c24f-11eb-9679-ed1a552de7a9.png" width ="300px">

&nbsp; 초기 단계에서는 자기자신을 루트노드로 가지고 있다. 유의할 점은 여기서의 부모 테이블은 부모에 대한 정보만을 담고 있다는 것이다. 다시 말해 특정 노드의 **루트**를 확인하고자 할때는 **재귀적으로 부모를 거슬러 올라가서** 최종적인 루트 노드를 찾아야한다. 


<table>
    <tbody>
        <tr>
            <td> <strong> [ step1 ]</strong><br><br>
            <img src="https://user-images.githubusercontent.com/70243735/120187562-e7acd280-c24f-11eb-9b07-3c98bdca9270.png" width="300px"> 
                <br> 1) 1의 루트 노드는 1이고, 4의 루트노드는 4이다. <br>2) 더 작은 루트노드인 1을 루트노드 4의 부모로 설정한다.
            </td>
            <td> <strong> [ step2 ]</strong><br><br>
            <img src="https://user-images.githubusercontent.com/70243735/120187812-46724c00-c250-11eb-98e3-c2bde15da3ea.png" width="300px"> 
                <br> 1) 2의 루트노드는 2이고, 3의 루트노드는 3이다. <br> 2) 더 작은 루트노트인 2을 루트노드 3의 부모로 설정한다.
            </td>
        </tr>
        <tr>
            <td> <strong> [ step3 ]</strong><br><br>
            <img src="https://user-images.githubusercontent.com/70243735/120187823-4a9e6980-c250-11eb-9796-82b503602159.png" width="300px"> 
                <br> 1) 2의 루트노드는 2이고, 4의 루트노드는 1이다. <br> 2) 더 작은 루트노드인 1을 루트노드 2의 부모로 설정한다.
            </td>
            <td><strong> [ step4 ]</strong><br><br>
            <img src="https://user-images.githubusercontent.com/70243735/120187849-525e0e00-c250-11eb-9f5d-1157749e84fe.png" width="300px"> 
                <br> <br> 1) 5의 루트노드는 5이고, 6의 루트노드는 6이다. <br> 2) 더 작은 루트노드인 5를 루트노드 6의 부모로 설정한다.
            </td>
        </tr>
    </tbody>
</table>

<br>
 

## 💡 Disjoint Sets 구현


```python
# 특정 원소가 속한 집합을 찾기위해서 루트노드를 반환하는 find연산
def find_parent(parent, x):
    
    # 루트노드가 아니라면, 루트 노드를 찾을 때까지 재귀적으로 호출
    if parent[x] != x:
        return find_parent(parent, parent[x])
    
    # 자신이 루트노드일때
    return x

# 두 원소가 속한 집합을 합치는 union연산
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

# 노드의 개수와 간선(union 연산)의 개수 입력받기
v, e = map(int, input().split())

# 부모테이블
parent = [i for i in range(v+1)] # 초기 상태에서 모든 노드의 루트노드는 자기자신

# union 연산을 각각 수행
for i in range(e):
    a,b = map(int, input().split())
    union_parent(parent, a, b)

# 각 원소의 루트노드를 출력
print("각 원소의 루트노드:", end=' ')
for i in range(1, v+1):
    print(find_parent(parent, i), end=' ')

print()

# 부모테이블 내용 출력
print("부모테이블:", end=' ')
for i in range(1, v+1):
    print(parent[i], end=' ')
```

입력&nbsp; &nbsp; |	출력
-|-|
6 4<br>1 4<br>2 3<br>2 4<br>5 6	| 각 원소의 루트노드: 1 1 1 1 5 5 <br>부모테이블: 1 1 2 1 5 5 

<br>

## 💡 경로 압축 기법
&nbsp; 위의 코드로 구현시에 답을 구할 수는 있지만, find함수가 비효율적으로 동작한다는 문제점이 있다. 루트 노드를 찾기위해서 **부모 테이블을 계속 확인하며 거슬러 올라가야하기 때문**이다. 최악의 경우 find함수가 모든 노드를 다 확인하는 터라 시간복잡도가 O(V)이다. 

&nbsp; 이러한 find함수를 경로 압축 기법(Path Compression)을 사용하면 시간복잡도를 개선할 수 있다. **부모 테이블에 루트노드를 바로 저장**하는 것이다. 경로 압축 기법을 사용하면 루트노드에 더욱 빠르게 접근할 수 있다. 앞선 예시들과 동일한 상황에 대해서 다음과 같이 설정이 된다.

<img src="https://user-images.githubusercontent.com/70243735/120188888-a3223680-c251-11eb-9e79-2b12672fa42b.png" width="300px">

&nbsp; 코드로 구현하게 되면 나머지는 모두 동일하고 find_parent()만 수정된다.
```python
# 특정 원소가 속한 집합을 찾기위해서 루트노드를 반환하는 find연산
def find_parent(parent, x):
    
    # 루트노드가 아니라면, 루트 노드를 찾을 때까지 재귀적으로 호출
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x]) # 부모를 루트노드로 변경
    
    return parent[x]
```

입력&nbsp; &nbsp; |	출력
-|-|
6 4<br>1 4<br>2 3<br>2 4<br>5 6	| 각 원소의 루트노드: 1 1 1 1 5 5 <br>부모테이블: 1 1 1 1 5 5 

<br>

## 💡 사이클 판별 알고리즘
&nbsp; Disjoint Sets는 다양한 알고리즘에 사용될 수 있다. 특히 **무방향 그래프** 내에서의 사이클을 판별할 때 사용될 수 있다. 참고로 방향그래프에서의 사이클 여부는 DFS를 이용해 판별할 수 있다.

**[ 동작 과정 ]**

1. 각 간선을 확인하며 두 노드의 루트노드를 확인한다.

2. **루트노드가 서로 다르다면** 두 노드에 대하여 union연산을 수행한다.

3. **루트노드가 서로 같다면** 사이클이 발생한 것이다.

4. 그래프에 포함되어있는 모든 간선에 대하여 1~3과정을 반복한다.

   : 만약 모든 간선이 처리될 때까지 사이클이 발생하지 않았다면, 해당 그래프에서는 사이클이 없다라고 판단될 수 있다.


<table>
    <tbody>
        <tr>
            <td> <strong> [ step0 ]</strong><br><br>
            <img src="https://user-images.githubusercontent.com/70243735/120188984-c351f580-c251-11eb-95b5-e5e69c794eb2.png" width="200px"> 
                <br> <br><br><br>
            </td>
            <td> <strong> [ step1 ]</strong><br><br>
            <img src="https://user-images.githubusercontent.com/70243735/120188996-c64ce600-c251-11eb-9d54-721b58f7b417.png" width="200px"> 
                <br> 1) 1의 루트노드는 1, 2의 루트노드는 2이다.<br> 2) 루트노드가 서로 다르기 때문에 두 노드에 대해 union연산을 수행한다.
            </td>
        </tr>
        <tr>
            <td width="400px"> <strong> [ step2 ]</strong><br><br>
            <img src="https://user-images.githubusercontent.com/70243735/120189010-c947d680-c251-11eb-97af-1822ec46832e.png" width="200px"> 
                <br> 1) 1의 루트노드는 1이고 3의 루트노드는 3이다.<br> 2) 루트노드가 서로 다르기 때문에 두 노드에 대해 union연산을 수행한다.
            </td>
            <td width="400px"><strong> [ step3 ]</strong><br><br>
            <img src="https://user-images.githubusercontent.com/70243735/120189029-cd73f400-c251-11eb-91ba-2df4461f0127.png" width="200px"> 
                <br> 1) 2의 루트노드는 1이고 3의 루트노드는 1이다.<br> 2) 루트노드가 서로 같다. 두 노드가 이미 같은 노드에 속해 있다는 뜻이고 해당 그래프에 사이클이 있다는 의미이다.
            </td>
        </tr>
    </tbody>
</table>

<br>

## 💡 사이클 판별 알고리즘 구현

```python
# 특정 원소가 속한 집합을 찾기위해서 루트노드를 반환하는 find연산
def find_parent(parent, x):
    
    # 루트노드가 아니라면, 루트 노드를 찾을 때까지 재귀적으로 호출
    if parent[x] != x:
    	parent[x] = find_parent(parent, parent[x]) # 부모를 루트노드로 변경
    
    return parent[x]

# 두 원소가 속한 집합을 합치는 union연산
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

# 노드의 개수와 간선(union 연산)의 개수 입력받기
v, e = map(int, input().split())

# 부모테이블
parent = [i for i in range(v+1)] # 초기 상태에서 모든 노드의 루트노드는 자기자신

# 사이클 발생 여부
cycle = False

# 모든 간선을 확인하며 사이클 발생 확인
for i in range(e):
    a,b = map(int, input().split())
    # 사이클이 발생한 경우 종료
    if find_parent(parent, a) == find_parent(parent, b):
        cycle = True
        break
    # 사이클이 발생하지 않았다면 union 수행
    else:
        union_parent(parent, a, b)
    union_parent(parent, a, b)

# 사이클 발생여부 출력
if cycle:
    print("사이클이 발생했습니다")
else:
    print("사이클이 발생하지 않았습니다")
```


입력&nbsp; &nbsp; |	출력
-|-|
3 3<br>1 2<br>1 3<br>2 3 |	사이클이 발생했습니다