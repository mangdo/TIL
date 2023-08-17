## 💡 트리

> 트리는 Node와 Branch를 이용해서, **사이클을 이루지 않도록** 구성한 데이터 구조이다.

&nbsp; 부모 노드 밑에 여러 자식 노드가 연결되고, 자식 노드 가각에 다시 자식노드가 연결되는 재귀적 형태의 자료구조이다. 이때 중요한 것은 자식 노드의 자식이 부모로 연결되는 경우는 트리로 간주 하지 않는다.(= 사이클을 이루지 않도록 한다)

<img src = https://github.com/mangdo/TIL/assets/70243735/7807617a-2169-457c-98bf-b80ab16ac962 width="450px">

<br>

- **Level** : 루트 노드부터 현재 노드까지의 깊이
- **Height** : 트리에서 노드가 가질 수 있는 최대 Level
- **Leaf Node (말단 노드)** : 자식이 없는 노드

<br>
<br>

## 💡 이진 트리
> 노드의 최대 브랜치가 2인 트리

[ 특징 ]

1. 이진트리에 있는 각 레벨의 최대 노드 개수는?

1               : Level 0 -> 1개
2 3             : Level 1 -> 2개
4 5 6 7         : Level 2 -> 4개
8 9 ... 14 15   : Level 3 -> 8개

Level K -> **2^k 개**

2. 높이가 h이고 꽉차있는 이진트리라면, 모든 노드의 개수는?

1 + 2^1 + 2^2 + 2^3 + 2^4 ..... 2^h 
**= 2^(h+1) -1 개**


3. 최대 노드의 개수가 N이라면 트리의 높이 h는?

2^{h+1} -1  = N → h = **log_{2}(N+1)-1**

<br>
<br>

## 💡 포화 이진 트리 (perfect binary tree)
> 모든 내부 노드가 두개의 자식 노드를 가지며, 모든 말단 노드(leaf node)는 동일한 레벨을 가지는 트리

<img src = https://github.com/mangdo/TIL/assets/70243735/8e99c6ec-86d4-454b-b526-390a7a62fb73 width="250px">


<br>
<br>


## 💡 완전 이진 트리 (complete binary tree)
> 마지막 레벨을 제외하고 모든 레벨이 완전히 채워져 있으며, 마지막 레벨의 노드는 가능한 가장 왼쪽에 있는 트리

<img src = https://github.com/mangdo/TIL/assets/70243735/cdf006ba-a5e3-48dc-a435-7f4af0bf821c width="250px">

<br>
<br>

## 💡 완전 이진 트리의 구현

완전 이진 트리의 경우, 클래스로 구현할 수도 있고 배열로도 구현할 수 있다.
위 그림의 완전 이진 트리는 [None, A, B, C, D, E]라는 배열로 표현할 수 있다.

배열에서 트리로 접근하려면 다음과 같은 규칙을 가진다.

1. 왼쪽 자식의 인덱스 : 현재 인덱스 * 2

2. 오른쪽 자식의 인덱스 : 현재 인덱스 * 2 + 1

3. 부모의 인덱스 : 현재 인덱스 // 2

예를 들어서 2번째 인덱스인 B의 왼쪽 자식은 D, 오른쪽 자식은 E 이다.

1. 왼쪽 자식 찾기    : 2 * 2 = 4,  인덱스 4의 값 D.

2. 오른쪽 자식 찾기 : 2 * 2 + 1 = 5,  인덱스 5의 값 E.

3. 인덱스 5의 부모 찾기 : 5 // 2 = 2,  인덱스2의 값 B.

<br>
<br>


## 💡 그외의 트리 종류

- [이진 탐색 트리](../Algorithm/binarySearch.md#-%EC%9D%B4%EC%A7%84-%ED%83%90%EC%83%89-%ED%8A%B8%EB%A6%AC) : 이진 탐색이 동작할 수 있도록 고안된 변형된 이진 트리

- 힙 : 데이터에서 최대값과 최소값을 빠르게 찾기 위해 고안된 변형된 완전 이진트리

- 힙 vs 이진 탐색트리
    - 공통점 : 둘다 이진트리
    - 차이점 
        1. 목적
        이진 탐색트리는 특정 노드를 빠르게 탐색하기 위한 구조, 힙은 최대 혹은 최소값을 탐색하기 위한 구조
        2. 최대/최소 값의 위치
        이진 탐색트리는 최대값이 우 최하단, 최소값은 좌 최하단이지만 힙은 최상단에 최대/최소 값이 위치


<br>
<br>

## 💡 완전 이진 트리 예시

### Q1. 업무 처리

&nbsp; 어떤 부서의 업무 조직은 완전이진트리 모양이다. 즉, 부서장이 루트이고 부서장 포함 각 직원은 왼쪽과 오른쪽의 부하 직원을 가진다. 부하 직원이 없는 직원을 말단 직원이라고 부른다.

&nbsp; 모든 말단 직원은 부서장까지 올라가는 거리가 동일하다. 조직도 트리의 높이는 H이다. 아래는 높이가 1이고 업무가 3개인 조직도를 보여준다.

<img src = "https://github.com/mangdo/TIL/assets/70243735/0816cd6c-0151-4efc-a442-3ed8bffa4109" width = "200px">

&nbsp; 업무는 R일 동안 진행된다. 처음에 말단 직원들만 각각 K개의 순서가 정해진 업무를 가지고 있다. 각 업무는 업무 번호가 있다. 각 날짜에 남은 업무가 있는 경우, 말단 직원은 하나의 업무를 처리해서 상사에게 올린다. 다른 직원들도, 대기하는 업무가 있는 경우 업무를 올라온 순서대로 하나 처리해서 상사에게 올린다. 단, 홀수 번째 날짜에는 왼쪽 부하 직원이 올린 업무를, 짝수 번째 날짜에는 오른쪽 부하 직원이 올린 업무를 처리한다.

&nbsp; 부서장이 처리한 일은 완료된 것이다. 업무를 올리는 것은 모두 동시에 진행한다. 따라서 그날 올린 업무를 상사가 처리하는 것은 그 다음날에야 가능하다.

&nbsp; 부서의 조직과 대기하는 업무들을 입력 받아 처리가 완료된 업무들의 번호의 합을 계산하는 프로그램을 작성하라


- 입력 조건
    - 첫 줄에 조직도의 높이 H, 말단에 대기하는 업무의 개수 K, 업무가 진행되는 날짜 수 R이 주어진다.
    - 그 다음 줄부터 각각의 말단 직원에 대해 대기하는 업무가 순서대로 주어진다. 제일 왼쪽의 말단 직원부터 순서대로 주어진다.

- 출력 조건
    - 완료된 업무들의 번호 합을 정수로 출력한다.


입력 예시 |출력 예시
-|-
1 1 1 <br> 1 <br> 2 | 0
1 3 2 <br> 9 3 7 <br> 5 11 2 | 5

<br>

**[ 문제 아이디어 ]**

우선 조직도를 완전 이진 트리로 구현해야한다. 부하 직원이 있는 직원들은, 각각 두 개의 큐를 가지고 있다. <br>
오른쪽 부하직원이 보낸 업무는 오른쪽 큐에 쌓아두고, 짝수번째 날짜에 하나를 꺼내 처리하고, 부모의 큐중 하나에 보낸다.




**[ 코드 ]**

```python

import sys
from collections import deque

height, works_count, working_day = map(int, sys.stdin.readline().split())

# 부하 직원이 있는 직원
lead_workers_count = (2**height) - 1 # h-1 만큼의 모든 노드
lead_workers = [[deque(), deque()] for _ in range(lead_workers_count + 1)]
lead_workers[0] = None

# 부하 직원이 없는 말단 직원
leaf_workers_count = 2**height
leaf_workers = [deque() for _ in range(leaf_workers_count)]
for i in range(leaf_workers_count):
    leaf_workers[i].extend(list(map(int, sys.stdin.readline().split())))


# 업무 시작
now_day = 1
ending_work = 0
while now_day <= working_day:
    # 맨 위 상사부터 일을 처리한다
    for i in range(1, lead_workers_count+1):
        # 짝수 번째 날짜에는 오른쪽 직원이 올린 업무 처리
        now_day_part = 1 if now_day % 2 == 0 else 0

        # 큐에 처리할 일이 있다면 처리하기
        if lead_workers[i][now_day_part]:
            leader_work = lead_workers[i][now_day_part].popleft()
            
            # 부서장이 처리한 일은 최종 완료
            if i == 1:
                ending_work += leader_work
            # 부서장이 아니면 상사에게 보낸다
            else:
                leader = i // 2
                position = 0 if i % 2 == 0 else 1
                lead_workers[leader][position].append(leader_work)
    

    # 말단 직원이 일을 처리하여 상사에게 보낸다
    for i in range(leaf_workers_count):
        if leaf_workers[i]:
            leaf_work = leaf_workers[i].popleft()

            # 해당 말단 직원의 상사
            leader = (i + lead_workers_count +1) // 2
            position = 0 if (i + lead_workers_count +1) % 2 == 0 else 1
            lead_workers[leader][position].append(leaf_work)


    now_day += 1

print(ending_work)

```

<br>

출처 : <br>
Softeer HSAT 5회 정기 코딩 인증평가 기출, 난이도 3 <br>
https://softeer.ai/practice/info.do?idx=1&eid=1256