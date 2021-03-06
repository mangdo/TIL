# 정렬 알고리즘

&nbsp; 정렬이란, 데이터를 특정한 기준에 따라서 순서대로 나열하는 것을 말한다. 다양한 정렬 알고리즘 중 주로 사용하는 것 들에는 선택 정렬, 삽입 정렬, 퀵 정렬, 계수 정렬이 있다. 정렬 수행시에는 상황에 맞는 알고리즘을 선택해야 효율적으로 작동할 수 있다.

-|선택 정렬   |삽입 정렬|퀵 정렬|병합정렬|계수 정렬|
-|-|-|-|-|-|
시간 복잡도	|O(N^2) |O(N^2) |O(NlogN)|O(NlogN)   |	O(N+K)
공간 복잡도	|O(N)	|O(N)	|O(N)|O(N)	    |O(N+K)
추천 상황   |	작은 범위, 간단	|거의 정렬되어 있는 경우|일반적인 경우|-|데이터 크기 범위가 작은 경우

(N : 데이터의 갯수, K : 데이터 최대값의 크기)

* 현재 예시들은 오름차순만 다루고 있다. *내림차순 정렬*은 알고리즘에서 크기 비교를 반대로 수행하거나 리스트의 원소를 뒤집어서 사용하면 된다. 리스트를 뒤집는 연산은 O(N)의 시간 복잡도를 가지고 있다.

<br>

## 💡 선택 정렬
> 현재 정렬되지 않은 데이터 중에서 가장 작은 데이터를 선택한다.

시간복잡도는 O(N^2)으로 비효율적이만, 코드 구현이 쉽다.

<img src="https://user-images.githubusercontent.com/70243735/119361465-a9ab2e00-bce6-11eb-8361-70e490ea3e8b.png" width ="600px">


**[ 코드 ]**   
이중 반복문을 사용하여 가장 작은 데이터를 찾아서 앞으로 보내는 과정을 반복한다.

```python
array = [6,3,2,1,4,5]

for i in range(len(array)):
  min_index = i # 가장 작은 데이터의 인덱스

  # 정렬되지 않은 데이터들 중
  for j in range(i+1, len(array)):
    # 더 작은 데이터를 찾았다면 인덱스를 변경해준다
    if array[min_index] > array[j]:
      min_index = j
  
  # 스와핑
  array[i], array[min_index] = array[min_index], array[i]

print(array)
```
<br>

## 💡 삽입 정렬
> 이미 정렬되어있는 데이터와 비교하여, 자신의 위치를 찾아 삽입한다.

&nbsp; 삽입 정렬의 시간복잡도는 O(N^2)이지만 데이터가 거의 정렬되어있다면 퀵 정렬 알고리즘보다도 빠르다. 최선의 경우O(N)의 시간복잡도를 가진다. 여기서 알아두어야할 점은 로 삽입 정렬은 두번째 데이터부터 시작된다는 것이다. 첫번째 데이터는 그자체로 정렬되어있다고 판단하기 때문이다.

<img src="https://user-images.githubusercontent.com/70243735/119362522-c09e5000-bce7-11eb-83f1-cf7fe015db2f.png" width="800px">

**[ 코드 ]**
```python
array = [6,3,2,1,4,5]

for i in range(len(array)):
  
  # 이미 정렬된 데이터들과 비교
  # 인덱스 i부터 1까지 감소하며 반복
  for j in range(i, 0, -1):
    # 정렬된 데이터보다 작다면 스와핑
    if array[j] < array[j-1]:
      array[j], array[j-1] = array[j-1], array[j]
    else: 
      break # 정렬된 데이터보다 크다면 멈춤

print(array)
```
<br>

## 💡 퀵 정렬
> 퀵정렬은 기준(pivot)을 설정한 다음 큰 수와 작은 수를 교환한 후 리스트를 반으로 나누는 방식으로 동작한다.

&nbsp; 퀵 정렬은 정렬 알고리즘 중에서도 가장 많이 사용되는 알고리즘 중 하나이다. 대부분의 프로그래밍 언어에서 정렬 라이브러리의 근간이 되는 알고리즘이기도 하다. **pivot**이란, 큰 숫자와 작은 숫자를 교환하기 위한 '기준'이다. 퀵 정렬을 수행하기 전에는 pivot을 어떻게 설정할 것인지를 미리 명시해야한다. pivot을 설정하고 분할하는 방법에 따라서 여러 방식으로 퀵정렬을 구분하는데, 현재 예시에서는 가장 대표적인 분할 방식인 호어 분할방식을 사용한다. 호어분할 방식에서는 리스트에서 첫번째 데이터를 pivot으로 설정한다. 

**[ 동작 과정 ]**

1. pivot을 설정

2. 왼쪽에서부터는 pivot보다 큰 데이터를 찾고, 오른쪽에서부터는 pivot보다 큰 데이터를 찾는다.

3. 찾은 큰데이터와 작은데이터를 서로 교환해준다. 

4. 2~3과정을 반복하다가 만약 두 데이터가 엇갈린 경우에는 '작은 데이터'와 pivot을 변경한다.

5. 이제 pivot의 왼쪽 데이터 리스트는 모두 pivot보다 작고, 오른쪽 데이터 리스트는 모두 pivot보다 크다.

6. 왼쪽 리스트와 오른쪽 리스트에 대해서 1~5과정을 다시 반복하다보면 모두 정렬된다.

<img src="https://user-images.githubusercontent.com/70243735/119363214-841f2400-bce8-11eb-888c-7577eaf6509a.png" width ="500px">

<img src="https://user-images.githubusercontent.com/70243735/119363260-913c1300-bce8-11eb-836b-f43b479c1993.png" width ="500px">

&nbsp; 개인적으로 엇갈리는 부분에서 이해가 어려웠는데 구체적인 동작은 코드로 보면 좀 더 이해할 수 있다. 유의해 둘 것은 5의 오른쪽 리스트 '876'에서 left는 리스트 밖까지 간다는 것이다. '67','34'에서 right는 pivot까지 간다. 코드에서 while구문 안에 left <= end와 right > start 부분을 보면 이를 알 수 있다.

**[ 코드 ]**

```python
array = [5,4,7,3,2,8,1,6]

def quick_sort(array, start, end):
  # 원소가 1개인 경우 종료
  if start >= end: 
      return
  
  pivot = start # pivot은 첫 번째 원소
  left = start + 1
  right = end

  # 엇갈리기 전까지 반복
  while(left <= right):
    # pivot보다 큰 데이터를 찾을 때까지 반복 
    while(left <= end and array[left] <= array[pivot]):
      left += 1
      print(left,end)

    # pivot보다 작은 데이터를 찾을 때까지 반복
    while(right > start and array[right] >= array[pivot]):
      right -= 1

    # 엇갈렸다면 작은 데이터와 pivot을 스와핑
    if(left > right):
      array[right], array[pivot] = array[pivot], array[right]
    else: 
      # 엇갈리지 않았다면 작은 데이터와 큰 데이터를 교체
      array[left], array[right] = array[right], array[left]

  # 분할 이후 왼쪽 부분과 오른쪽 부분에서 다시 퀵 정렬 수행
  quick_sort(array, start, right - 1)
  quick_sort(array, right + 1, end)

quick_sort(array, 0, len(array) - 1)
print(array)
```
**[ 퀵 정렬의 시간복잡도 ]**

&nbsp; 퀵 정렬의 평균 시간 복잡도는 **O(NlogN)**이다. pivot을 잘못 설정하는 **최악의 경우에는 O(N^2)** 시간복잡도를 가질 수도 있다. 예를 들어 퀵 정렬 중 호어분할 방식을 선택했을때 이미 '데이터가 정렬되어있는 경우'에는 매우 느리게 동작한다. 앞서 삽입 정렬은 데이터가 정렬되어있는 경우에 매우 빠르게 동작하는 것과 반대된다. 실제로 c++과 같은 퀵 정렬을 기반으로 작성된 정렬 라이브러리를 제공하는 프로그래밍언어들은 최악의 경우에도 시간 복잡도가 O(NlogN)이 되는 것을 보장할 수 있도록 pivot값을 설정하는 추가적인 로직을 더해준다.

<br>


## 💡 병합 정렬(Merge Sort)
> 정렬되어있는 두 집합을 합쳐가며 정렬하는 알고리즘

&nbsp; 퀵 정렬과 마찬가지로 시간복잡도가 **O(NlogN)이고 분할-정복 방식**이다. 하지만 퀵정렬의 최악의 시간복잡도가 O(N^2)가 였던 것에 반해, 병합 정렬은 **최악의 시간복잡도도 O(NlogN)**이다. 그럼에도 불구하고 실제 구현을 해보면 거의 모든 경우에 퀵정렬이 우세하다고 나온다. 왜냐하면 합병정렬의 경우에는 배열을 생성하는 시간이 있기때문이다. 이는 정렬하려는 배열의 길이가 길수록 더 차이가 난다.


**[ 동작 과정 ]**

1. 중간을 기준으로 오른쪽과 왼쪽, 2개의 배열로 분할시켜 나갑니다.   
  : 부분 배열의 길이가 1이 될때까지 재귀호출을 반복시킵니다. 만약 길이가 1이라면 해당 배열을 정렬되어있다라고 생각할 수 있습니다.

2. 정렬되어있는 두 배열을 합치며 완성된 배열을 만들어냅니다.


- 분할

  <img src="https://user-images.githubusercontent.com/70243735/121863791-2b670800-cd37-11eb-9e7d-c4e5d7c8b43d.png" width="500px">

- 정복

  <img src="https://user-images.githubusercontent.com/70243735/121863865-3fab0500-cd37-11eb-92a3-376cce0251a7.png" width="500px">


**[ 코드 ]**

```python
give_array = [5, 3, 2, 1, 6, 8, 7, 4]

def merge_sort(array):
    if len(array) <= 1:
        return array
    mid = len(array)//2
    left_array = merge_sort(array[:mid])
    right_array = merge_sort(array[mid:])
    return merge(left_array, right_array)

def merge(array1, array2):
    result = []
    array1_index = 0
    array2_index = 0
    # 정렬되어 있는 두 리스트를 합치기
    while array1_index < len(array1) and array2_index < len(array2):
        if array1[array1_index] < array2[array2_index]:
            result.append(array1[array1_index])
            array1_index += 1
        else:
            result.append(array2[array2_index])
            array2_index += 1

    result = result+array1[array1_index:] + array2[array2_index:]
    return result

print(merge_sort(give_array))
```


<br>


## 💡 계수 정렬
> 데이터의 크기 범위가 작을때, 사용할 수 있는 매우 빠른 정렬 알고리즘이다.

&nbsp; 일반적으로 **데이터 크기 범위가 1,000,000(백만)을 넘지 않을때만 사용**할 수 있다. 계수 정렬은 앞서 다루었던 선택/삽입/퀵 정렬은 직접 데이터의 값을 비교한뒤에 위치를 변경하며 정렬하는 방식과는 다르다. 

**[ 동작 방식 ]**

1. 가장 큰 데이터와 가장 작은 데이터의 범위가 모두 담길 수 있는 리스트를 생성한다

2. 데이터를 하나씩 확인하며, 데이터의 값과 동일한 인덱스의 데이터를 1씩 증가시킨다.

만약 [2,3,1,6,8,8,8,4,3,2]라는 데이터가 주어졌다면 다음과 같은 리스트가 생성된다.


인덱스	|0	|1	|   2|  3|	4|	5|	6|	7|	8|
-|         -|  -|   -|  -|  -|  -|  -|  -|  -|
갯수	|0	|1	|   2|  2|	1|	0|	1|	0|	3|

이에 대한 출력결과는 1223346888이된다.


**[ 코드 ]**

```python
# 모든 원소의 값이 0보다 크거나 같다고 가정
array = [2,3,1,6,8,8,8,4,3,2]

# 모든 범위를 포함하는 리스트 선언(모든 값을 0으로 초기화)
count = [0]*(max(array)+1)

# 데이터를 하나씩 확인
for i in range(len(array)):
  count[array[i]] += 1 # 각 데이터 값에 해당하는 인덱스의 데이터 증가

# 리스트 기반으로 출력
for i in range(len(count)):
  # 인덱스 데이터만큼 출력
  for j in range(count[i]):
    print(i, end=' ')
```

**[ 계수 정렬의 시간복잡도 ]**

&nbsp; 데이터의 갯수를 M, 데이터의 최대값 크기를 K라고 할때, 계수 정렬의 시간복잡도는 O(N+K)로 이제까지 살펴본 정렬 알고리즘 중 가장 빠르다. 하지만 데이터의 최대값 크기만큼의 메모리가 필요하기 때문에 심각한 비효율성을 초래할 수 있다. 예를 들어 10,000,000와 1로 단 2개의 데이터를 가지고 있을때도 10,000,001크기의 리스트를 선언해야한다. 때문에 계수 정렬은 데이터의 크기 범위가 작을때만 사용하는 것이 좋다. 

<br> 


## 💡 파이썬 정렬 라이브러리

&nbsp; 지금까지 다양한 정렬 알고리즘에 대해서 알아보았다. 알고리즘 문제를 풀때는 직접 정렬 알고리즘을 구현해서 사용하는 경우도 있지만 미리 만들어진 라이브러리를 이용하는 것이 효과적인 경우가 더 많다. 파이썬은 기본 정렬 라이브러리인 sorted()함수를 제공한다. sorted는 퀵 정열과 동작 방식이 비슷한 병합 정렬을 기반으로 만들어졌다. 병합정렬은 일반적으로 퀵정렬보다 느리지만 최악의 경우에도 시간복잡도 O(NlogN)을 보장한다는 특징이 있다.

* sorted()

리스트, 집합, 딕셔너리 자료형 등을 입력받아서 정열된 결과를 출력한다. set이나 dictionary자료형을 사용해도 반환되는 결과는 리스트 자료형임을 주의해야한다.
```python
array = [2,3,1,4,5]

result = sorted(array)
print(result)
```
* sort()

리스트 객체의 내장함수이다. sort()는 별도의 반환 값이 없고, 내부 원소가 바로 정렬된다.
```python
array = [2,3,1,4,5]

array.sort()
print(array)
```

* key⭐

&nbsp; sorted()나 sort()를 이용할 때에는 key 매개변수를 입력으로 받을 수 있다. key값으로는 하나의 함수가 들어가야하며 이는 정렬 기준이 된다. 다음 코드는 리스트가 튜플로 구성되어있을 때 각 데이터의 두번째 원소를 기준으로 정렬하는 코드이다.

```python
array = [('바나나', 2), ('사과', 1), ('당근', 3)]

def setting(data):
  return data[1]

result = sorted(array, key=setting)
print(result)
```

* key에 람다함수 사용

```python
array = [('바나나', 2), ('사과', 1), ('당근', 3)]
# (lambda 매개변수 : 함수의 반환값)
result = sorted(array, key=lambda data:data[1])
print(result)
```

<img src="https://user-images.githubusercontent.com/70243735/119364769-33a8c600-bcea-11eb-8687-15962c023173.png">
 

<br>

출처 :   
이것이 코딩테스트다(이동빈 저)