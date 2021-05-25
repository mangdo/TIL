# 이진 탐색 알고리즘

> 탐색 범위를 반으로 좁혀가며 빠르게 탐색하는 알고리즘이다.   
&nbsp; 단, 데이터가 정렬되어 있어야지만 사용할 수 있다. 순차탐색의 시간 복잡도는 O(N)이지만 이진탐색의 시간복잡도는 O(logN)으로 빠르게 탐색이 가능하다. 만약 데이터의 탐색 범위가 2,000만이 넘어가면 이진탐색으로 문제에 접근해보는 것이 좋다.

<br>

## 💡 이진 탐색 동작과정

1. 시작점과 끝점 사이의 중간점을 지정한다. 중간점이 실수라면 소수점 이하는 버린다.

2. 중간점과 찾으려는 데이터를 비교한다.

3. 찾으려는 데이터가 중간점보다 크다면 시작점을 중간점 이후로 변경한다.

4. 찾으려는 데이터가 중간점보다 작다면 끝점을 중간점 이후로 변경한다.

5. 찾으려는 데이터가 중간점과 일치할때까지 1~4과정을 반복한다.

찾으려는 데이터가 2일때 동작과정은 다음과 같다.

<img src="https://user-images.githubusercontent.com/70243735/119479831-001e7800-bd8c-11eb-8725-46d52289b983.png" width="500px">

<br> 

## 💡 이진 탐색 구현 코드

**[ 반복문로 구현하는 방법 ]**

```python
def binary_search(array, target, start, end):
    while start<=end:
        mid = (start+end)//2 # 소수점 이하는 버림
        
        # 탐색성공
        if array[mid] == target: 
            return mid
        # 중간점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
        elif array[mid] > target:
            end = mid-1
        # 중간점 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
        else:
            start = mid+1
    return None # 탐색이 끝났으나 찾지 못했다.
 
```

**[ 재귀함수를 구현하는 방법 ]**

```python
def binary_search(array, target, start, end):
    if start>end:
        return None
    mid = (start+end)//2 # 소수점 이하 버림
    
    if array[mid] == target: #탐색 성공
        return mid
    # 중간점값보다 작다면 왼쪽 확인
    elif array[mid]>target:
        return binary_search(array, target, start, mid-1)
    # 중간점값보다 크면 오른쪽 확인
    else: 
        return  binary_search(array, target, mid+1, end)
```

<br>


## 💡 이진 탐색 트리
> 이진 탐색 트리는 이진 탐색이 동작할 수 있도록 고안된, 효율적인 탐색이 가능한 자료구조이다.

**트리**란, Node와 Branch를 이용해서, 사이클을 이루지 않도록 구성한 데이터 구조를 의미한다.   
**이진 트리**란, Node의 Branch가 2인 트리를 의미한다.  
마지막으로 **이진 탐색 트리**는 다음과 같은 추가적인 조건이 있는 이진트리이다.   
1) 모든 노드는 왼쪽 가지에 포함되는 어떠한 숫자보다도 크다.
2) 모든 노드는 오른쪽 가지에 포함되는 어떠한 숫자보다도 작다.

<img src="https://user-images.githubusercontent.com/70243735/119479866-0a407680-bd8c-11eb-97f3-99b2540cbb4f.png" width="400px">

<br>

## 💡 파이썬 이진 탐색 라이브러리
&nbsp; 파이썬에서는 이진 탐색을 쉽게 구현할 수 있도록 bisect 라이브러리를 제공한다. 이를 이용해서 정렬된 배열에서 특정 범위에 속하는 데이터 갯수를 구하거나 특정 값의 데이터 갯수를 구할 수 있다.

- bisect_left(a, x) : 리스트 a에 데이터 x를 삽입할 가장 왼쪽 인덱스를 찾는 메소드   
- bisect_right(a, x) : 리스트 a에 데이터 x를 삽입할 가장 오른쪽 인덱스를 찾는 메소드

<img src="https://user-images.githubusercontent.com/70243735/119479876-0e6c9400-bd8c-11eb-996e-61e1abbbf763.png" width="400px">

``` python
from bisect import bisect_left, bisect_right

def count_by_range(a, left_value, right_value):
    left_index = bisect_left(a, left_value)
    right_index = bisect_right(a, right_value)
    return right_index - left_index
    
a = [1,2,4,4,5]

# 값이 4인 데이터 갯수
print(count_by_range(a,4,4))
# 값이 4~5인 데이터 갯수
print(count_by_range(a,4,5))
 
```
<br>

## 💡 이진 탐색 알고리즘 문제
### Q1. 떡볶이 떡 만들기
&nbsp; 동빈이네 떡볶이 떡은 떡볶이 떡의 길이가 일정하지 않다. 대신에 한봉지 안에 들어가는 떡의 총길이는 절단기로 잘라서 맞춰준다. 절단기에 높이 (H)를 지정하면 줄지어진 떡을 한번에 절단한다. 높이가 H보다 긴 떡은 H위의 부분이 잘릴 것이고 낮은 떡은 잘리지 않는다.    
예를 들어 높이가 19, 14, 10, 17cm인 떡이 나란히 있고 절단기 높이를 15cm라고 하면 자른 뒤 떡의 높이는 15, 14, 10, 15cm가 될 것이다. 잘린 떡의 길이는 차례대로 4, 0, 0, 2cm이다. 손님은 6cm만큼의 길이를 가져간다.   
손님이 왔을 때 요청한 총 길이가 M일때 적어도 M만큼의 떡을 얻기 위해 절단기에 설정할 수 있는 높이의 최댓값을 구하는 프로그램을 작성하시오.

* 입력 조건
    - 첫째줄에 떡의 갯수 N과 요청한 떡의 길이 M이 주어진다. (1<=N<=1,000,000, 1<=M<=2,000,000,000)
    - 둘째줄에는 떡의 개별 높이가 주어진다. 떡 높이의 총합은 항상 M이상이므로, 손님은 필요한 양만큼 떡을 사갈 수 있다. 높이는 10보다 작거나 같은 양의 정수 또는 0이다.

* 출력 조건
    - 적어도 M만큼의 떡을 집에 가져가기 위해 절단기에 설정할 수 있는 높이의 최댓값을 출력한다.

 

* 입력 예시
    ```
    4 6
    19 15 10 17
    ```

* 출력 예시
    ```
    15
    ```

**[ 문제 아이디어 ]**   
절단기에 설정할 수 있는 높이(H)의 범위는 1~ 요청한 떡의 길이(M)까지이다.   
이때 요청한 떡의 길이(M)의 **범위가 20억**까지이기 때문에 순차탐색이아닌 이진탐색으로 접근해야한다.

**[ 코드 ]**

```python
n, m = map(int, input().split())
rice = list(map(int, input().split()))

start = 0
end = max(rice)
result = 0

# 절단기 높이 이진 탐색
# 연산을 수행할 수록 최적화된 값을 찾을 수 있다
while start <= end:
    h = (start+end)//2
    total = 0
    
    # 정한 절단기 높이 값으로 잘라본다
    for i in range(n):
        # 절단기 높이 보다 긴 떡만 자른다
        if rice[i] > h:
            total += rice[i] - h
        
    # 손님이 원하는 값에 정확히 일치
    if total == m:
        break
    # 손님이 원하는 떡이 충분하다
    elif total > m:
        # 줄 수는 있는 상황이지만 더 적게 남기는 절단기 높이를 탐색
        start = h+1
        result = h # 줄 수는 있으니 일단 저장해놔야한다
    # 손님이 원하는 떡이 부족하다
    else :
        end = h-1
        
print(h)
```

<br>
 

출처:   

이것이 코딩테스트다(이동빈 저)