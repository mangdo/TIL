# 💡 다익스트라 최단 경로 알고리즘

&nbsp; **하나의 출발 노드**로 부터 다른 **모든 노드까지의 최단거리**를 구하는 알고리즘이다. 단, *'음의 간선'*이 없을 때만 정상적으로 동작한다. 다익스트라가 연구한 알고리즘 중 가장 대표적인 알고리즘이기 때문에 간단하게 다익스트라 알고리즘이라고도 불린다. 다익스트라 알고리즘은 기본적으로 그리디 알고리즘으로 분류된다. 매번 가장 비용이 가장 적은 노드를 선택하는 과정을 반복하기 때문이다.

<br>

## 💡 다익스트라 알고리즘 동작과정

1. 출발 노드를 설정한다
2. 최단거리 테이블을 초기화한다.
    -> 다른 모든 노드로 가는 최단거리를 '무한'으로 초기화한다
3. 방문하지 않은 노드 중에서 **최단거리가 가장 짧은 노드**를 선택한다.
    -> 이때 선택된 노드의 최단거리는 확정된다.
4. 해당 노드를 거쳐 다른 노드로 가는 비용를 게산하여 **최단 거리 테이블**을 갱신한다.
5. 3~4 과정을 반복한다.

<img src="https://user-images.githubusercontent.com/70243735/119837822-e2911000-bf3d-11eb-89de-0bdc1cc2f982.png" width="700px">

<img src="https://user-images.githubusercontent.com/70243735/119837864-e9b81e00-bf3d-11eb-8836-3d1089aa6061.png" width="700px">

<br>

## 💡 다익스트라 알고리즘 : 순차탐색

&nbsp; 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택하기 위해 순차 탐색을 이용하여 코드로 구현할 수 있다. 이때 시간복잡도는 O(N^2)이다. 총 O(N)번에 걸쳐 **가장 짧은 노드를 매번 선형탐색**해야하고 현재 노드와 연결된 노드를 모두 확인해야하기 때문이다. 따라서 전체 노드의 수가 5,000개 이하라면 순차탐색 방법을 써도 괜찮지만 그 이상이라면 힙을 사용하는 개선된 다익스트라 알고리즘을 이용해야한다.

```python
import sys

input = sys.stdin.readline # 빠른 입력
INF = int(1e9) # 무한을 의미하는 값으로 10억 설정

# 노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
# 시작 노드 번호를 입력받기
start = int(input())
# 방문 체크
visited = [False]*(n+1)
# 최단거리 테이블
distance = [INF]*(n+1)

# 노드 연결정보
graph = [[] for i in range(n+1)]

for _ in range(m):
  # a번노드에서 b번 노드로 가는 비용c
  a,b,c = map(int, input().split())
  graph[a].append((b,c))

# 방문하지 않은 노드 중 가장 최단거리가 짧은 노드의 번호를 반환
def get_smallest_node():
  min_value = INF
  index = 0
  for i in range(1, n+1):
    if distance[i] < min_value and not visited[i]:
      min_value = distance[i]
      index = i
  return index

# 다익스트라 알고리즘
def dijkstra(start):
  # 시작 노드
  distance[start] = 0
  visited[start] = True
  # 출발노드와 인접노드에 대해 최단거리 테이블 갱신
  for j in graph[start]:
    distance[j[0]] = j[1]

  # 모든 노드에 대해 반복
  for i in range(n-1):
    # 현재 최단거리가 가장 짧은 노드를 꺼내서 방문처리
    now = get_smallest_node()
    visited[now] = True
    # 선택된 노드와 연결된 다른 노드를 확인
    for j in graph[now]:
      # 선택된 노드를 통해 가는 비용을 다시 계산
      # 선택된 노드의 비용 + 연결된 노드로 가는 비용
      cost = distance[now] + j[1]
      # 선택된 노드를 거쳐서 가는 비용이 더 짧은 경우
      if cost<distance[j[0]]:
        distance[j[0]] = cost # 최단거리 테이블 갱신
  
#다익스트라 알고리즘수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n+1):
  # 도달할 수 없는 경우
  if distance[i] == INF:
    print("infinity")
  else:
    print(distance[i])
```

<br>

## 💡 다익스트라 알고리즘 : 최소힙

&nbsp; 방문하지 않은 노드 중 최단거리가 가장 짧은 노드를 선택하기 위해 최소 힙을 사용한다.   
&nbsp; 파이썬의 heapq라이브러리는 원소로 튜플을 받으면 튜플의 첫번째 원소를 기준으로 우선순위 큐를 구성한다. 따라서 (거리, 노드 번호) 순서대로 튜플 데이터를 구성해 **최소 힙에 넣으면 거리순으로 정렬**된다. 힙에서 노드를 꺼냈는데 만약 해당 노드를 이미 처리한적이 있다면 무시하고 아직 처리하지 않은 노드에 대해서만 처리하면된다.

```python
import heapq
import sys

input = sys.stdin.readline # 빠른 입력
INF = int(1e9) # 무한을 의미하는 값으로 10억 설정

# 노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
# 시작 노드 번호를 입력받기
start = int(input())
# 최단거리 테이블
distance = [INF]*(n+1)

# 노드 연결정보
graph = [[] for i in range(n+1)]

for _ in range(m):
  # a번노드에서 b번 노드로 가는 비용c
  a,b,c = map(int, input().split())
  graph[a].append((b,c))

# 다익스트라 알고리즘(최소힙 이용))
def dijkstra(start):
  q=[]
  # 시작 노드
  heapq.heappush(q, (0,start))
  distance[start] = 0

  while q:
    # 가장 최단거리가 짧은 노드에 대한 정보 꺼내기
    dist, now = heapq.heappop(q)

    # 이미 처리된 노드였다면 무시
    # 별도의 visited 테이블이 필요없이, 최단거리테이블을 이용해 방문여부 확인
    if distance[now] < dist:
      continue
    # 선택된 노드와 인접한 노드를 확인
    for i in graph[now]:
      cost = dist + i[1]
      # 선택된 노드를 거쳐서 이동하는 것이 더 빠른 경우
      if cost < distance[i[0]]:
        distance[i[0]] = cost
        heapq.heappush(q, (cost,i[0]))
  
# 다익스트라 알고리즘수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n+1):
  # 도달할 수 없는 경우
  if distance[i] == INF:
    print("infinity")
  else:
    print(distance[i])
```
<br>

## 💡 다익스트라 알고리즘 예시
### Q1. 전보
&nbsp; &nbsp; 어떤 나라에는 N개의 도시가 있다. 각 도시는 보내고자 하는 메시지가 있는 경우, 다른 도시로 전보를 보내서 다른 도시로 해당메시지를 전송할 수 있다. 하지만 X라는 도시에서 Y라는 도시로 전보를 보내고자 한다면, 도시 X에서 Y로 향하는 통로가 설치되어있어야한다. 예를 들어 X에서 Y로 향하는 통로는 있지만 Y에서 X로 향하는 통로가 없다면 Y는 X로 메시지를 보낼 수 없다. 또한 통로를 거쳐 메시지를 보낼 때는 일정한 시간이 소요된다.

&nbsp; 어느날 C라는 도시에서 위급상황이 발생했다. 최대한 많은 도시로 메시지를 보내고자 한다. 메시지는 도시 C에서 출발하여 각 도시 사이에 설치된 통로를 거쳐 최대한 많이 퍼져나가야한다. 각 도시의 번호와 통로가 설치되어있는 정보가 주어졌을때 도시 C에서 보낸 메시지를 받게되는 도시의 개수는 총 몇개이며, 도시들이 모두 메시지를 받는데까지 걸리는 시간은 얼마인지 계산하는 프로그램을 작성하시오.

* 입력조건
    - 첫째줄에 도시의 갯수N, 통로의 갯수 M, 메시지를 보내고자 하는 도시C가 주어진다. (1<=N<=30,000, 1<=M<=200,000, 1<=C<=N)

    - 둘째줄부터 M+1번째 줄에 걸쳐서 통로에 대한 정보 X,Y,X가 주어진다. 이는 특정 도시 X에 다른 특정 도시 Y로 이어지는 통로가 있으며 메시지가 전달되는 시간이 Z라는 의미이다. (1=X,Y<=N, 1<=Z<=10,000)
* 출력조건
    - 첫째줄에 도시 C에서 보낸 메시지를 받는 도시의 총 개수와 총 걸리는 시간을 공백으로 구분하여 출력한다.

입력 예시	|출력 예시
-|-|
6 11<br>1<br>1 2 2<br>1 3 5<br>1 4 1<br>2 3 3<br>2 4 2<br>3 2 3<br>3 6 5<br>4 3 3<br>4 5 1<br>5 3 1<br>5 6 2 | 0<br>2<br>3<br>1<br>2<br>4

<br>

**[ 문제 아이디어 ]**

한 도시에서 다른 도시까지의 최단거리 문제를 묻는 문제이다. 이때 N,M의 범위가 크기 때문에 힙을 사용한 다익스트라 알고리즘으로 해결해야한다. 

**[ 코드 ]**

```python
import heapq
import sys

input = sys.stdin.readline # 빠른 입력
INF = int(1e9) # 무한을 의미하는 값으로 10억 설정

# 노드의 개수, 간선의 개수, 시작노드를 입력받기
n, m, start = map(int, input().split())

# 최단거리 테이블
distance = [INF]*(n+1)

# 노드 연결정보
graph = [[] for i in range(n+1)]

for _ in range(m):
  # x번노드에서 y번 노드로 가는 비용z
  x,y,z = map(int, input().split())
  graph[x].append((y,z))

# 다익스트라 알고리즘(최소힙 이용))
def dijkstra(start):
  q=[]
  # 시작 노드
  heapq.heappush(q, (0,start))
  distance[start] = 0

  while q:
    # 가장 최단거리가 짧은 노드에 대한 정보 꺼내기
    dist, now = heapq.heappop(q)

    # 이미 처리된 노드였다면 무시
    # 별도의 visited 테이블이 필요없이 최단거리테이블을 이용해 방문여부 확인
    if distance[now]<dist:
      continue
    
    # 선택된 노드와 인접한 노드를 확인
    for i in graph[now]:
      cost = dist + i[1]
      # 선택된 노드를 거쳐서 이동하는 것이 더 빠른 경우
      if cost < distance[i[0]]:
        distance[i[0]] = cost
        heapq.heappush(q, (cost,i[0]))
  
#다익스트라 알고리즘수행
dijkstra(start)

count = 0
max_distance = 0

for d in distance:
  if d!= INF:
    count+=1
    max_distance = max(max_distance, d)

## 시작노드는 제외해야함으로 count-1
print(count-1, max_distance)
```