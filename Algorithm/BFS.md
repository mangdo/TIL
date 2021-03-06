# BFS 알고리즘
> Breath-First Search

&nbsp; 그래프에서 **가까운 부분을 우선적으로 탐색**하는 알고리즘이다.너비 우선 탐색이라고도 한다. 데이터가 N개 있을때 O(N)의 시간 복잡도를 가진다. 일반적인 경우 실제 수행시간은 DFS보다 좋은편이다.

**[DFS vs BFS]**

-|동작 방식|동작 원리|구현|인접한 노드가 여러개라면?
-|-|-|-|-|
DFS|멀리 있는(깊게 있는)노드 부터 탐색|	스택|	재귀 함수 이용|	한개씩 넣음
BFS|	가까운 노드부터 탐색|	큐|	큐 자료구조 이용|	한번에 다 넣음|

<br>

## 💡 BFS 동작과정
1. 탐색 시작 노드를 큐에 삽입하고 방문 처리를 한다.

2. 큐에서 노드를 꺼내 해당 노드의 **인접노드 중에서 방문하지 않은 노드**를 **모두 큐에 삽입**하고 방문처리를 한다.

3. 2번과정을 더이상 수행할 수 없을 때까지 반복한다.

<img src="https://user-images.githubusercontent.com/70243735/119265418-9d10d200-bc21-11eb-84ea-bcf268fe4a53.png" width="700px">



결과적으로 노드의 탐색순서(큐에 들어간 순서)는 다음과 같다.   
`1->(2->3->8)->(7->4->5)->6`   
&nbsp; (2, 3, 4)는 모두 거리가 1이고, (7, 4, 5) 모두 거리가 2이고, 6는 거리가 3이다. 즉, 거리순으로 정렬된다. 이러한 특성을 이용해서 각 간선 비용이 모두 같다는 가정하에 최단거리 문제에도 사용될 수 있다.

<br>

## 💡 BFS 구현 코드
visited라는 리스트에 방문 여부를 저장했고 Queue를 사용한다.

```python
from collections import deque

# BFS
def bfs(graph, start, visited):
  # 큐 구현을 위해 deque라이브러리 사용
  queue = deque([start])

  # 탐색 시작 노드를 방문 처리
  visited[start] = True

  # 큐가 빌 때까지 반복
  while queue:
    # 큐에서 하나의 원소를 꺼내서 출력
    n = queue.popleft()
    print(n, end=' ')

    # 꺼낸 원소와 인접노드 확인
    for i in graph[n]:
      # 아직 방문하지 않은 노드라면
      if not visited[i]:
        queue.append(i)
        visited[i]=True

# 2차원 맵정보 입력받기
graph=[
  [], # 0번 노드 비우기
  [2,3,8], #1번 노드와 연결된 2,3,8노드
  [1,7],
  [1,4,5],
  [3,5],
  [3,4],
  [7],
  [2,6,8],
  [1,7]
]

# 방문 정보
visited = [False]*(8+1) #(총 노드의 갯수)+인덱스 0
# bfs호출
bfs(graph, 1, visited) # 1 2 3 8 7 4 5 6 출력
```

<br>

## 💡 BFS 구현 코드 2
동일하게  Queue를 사용하지만 visited라는 리스트에 **방문 순서대로 노드를 저장**하고 not in, in을 이용한다.

```python
from collections import deque

def bfs(graph, start):
    queue = deque([start])
    visited = []

    # 큐가 빌 때까지
    while queue:
        cur_node = queue.popleft()
        visited.append(cur_node)

        # 꺼낸 원소와 인접노드 확인
        for link_node in graph[cur_node]:
            # 아직 방문하지 않은 노드라면 큐에 담아줌
            if link_node not in visited and link_node not in queue:
                queue.append(link_node)
    return visited

# 2차원 맵정보 입력받기
graph=[
  [], # 0번 노드 비우기
  [2,3,8], #1번 노드와 연결된 2,3,8노드
  [1,7],
  [1,4,5],
  [3,5],
  [3,4],
  [7],
  [2,6,8],
  [1,7]
]

# bfs 수행
visited_bfs = bfs(graph, 1)
for i in visited_bfs:
    print(i, end=" ") # 1 2 3 8 7 4 5 6 출력

```
<br>

## 💡 BFS 알고리즘 문제

### Q1. 미로 탈출
&nbsp; 동빈이는 N*M 크기의 직사각형 형태의 미로에 갇혀있다. 미로에는 여러 마리의 괴물이 있어 이를 피해 탈출해야한다. 동빈이의 위치는 (1,1)이고 미로의 출구는 (N,M)의 위치에 존재하며 한번에 한칸씩 이동할 수 있다. 이때 괴물이 있는 부분은 0으로, 괴물이 없는 부분은 1로 표시되어있다. 미로는 반드시 탈출할 수 있는 형태로 제시된다. 이때 동빈이가 탈출하기 위해 움직여야하는 최소 칸의 개수를 구하시오. 칸을 셀때는 시작 칸과 마지막 칸을 모두 포함해서 계산한다.

* 입력 조건
    - 첫째줄에 두 정수 N,M(4<= N,M <= 200)이 주어집니다. 다음 N개의 줄에는 각각 M의 정수(0혹은 1)로 미로의 정보가 주어진다. 각각의 수들은 공백 없이 붙어서 입력으로 제시된다. 또한 시작 칸과 마지막 칸은 항상 1이다.

* 출력 조건
    - 첫째줄에 최소 이동 칸의 개수를 출력한다.



* 입력 예시
    ```
    5 6
    101010
    111111
    000001
    111111
    111111
    ```
* 출력 예시
    ```
    10
    ```


### [문제 아이디어]

&nbsp; BFS는 가까운 거리순으로 탐색하기 때문에 최단 거리 문제에도 사용될 수 있다. **방문한 노드의 값을 거리 정보로 변경**한다.
그러면 한번도 방문하지 않은 곳을 1, 가지 못할 곳은 0, 이미 간 곳은 1보다 큰 값이된다.

<img src="https://user-images.githubusercontent.com/70243735/119265663-730bdf80-bc22-11eb-9db4-70d486e13966.png" width="700px">

### [코드]

&nbsp; 구현시, visited 리스트가 따로 필요하지 않다.
미로의 정보를 담은 graph를 한번도 방문하지 않은 곳을 1, 가지 못할 곳은 0으로 유지하고 이미 간 곳은 1보다 큰값으로 갱신하기 때문이다.

```python
from collections import deque

# n개의 줄, m개의 열
n, m = map(int,input().split())

# 미로의 정보 입력받기
graph=[]
for i in range(n):
  graph.append(list(map(int,input())))

# 방향 정보(상하좌우)
dx = [-1,1,0,0]
dy = [0,0,-1,1]

# 출발 노드
queue = deque()
deque.append((0,0))
# 혹은 deque([(0,0)])

while queue :
  # 큐에서 하나의 원소를 꺼내서 출력
  x, y = queue.popleft()

  # 꺼낸 원소와 인접노드 확인
  for i in range(len(dx)):
    nx = x+dx[i]
    ny = y+dy[i]

    # 범위를 벗어난 노드 무시
    if nx>n-1 or ny>m-1 or nx<0 or ny<0 :
      continue

    # 아직 방문하지 않은 노드라면
    # 처음 방문하는 경우가 바로 최단거리다
    if graph[nx][ny]==1:
      queue.append((nx,ny))
      graph[nx][ny] = graph[x][y]+1 # 직전 노드+1


print(graph[n-1][m-1])
```

<br>

출처 :   
이것이 코딩테스트다(이동빈 저)