# 💡 다이나믹 프로그래밍
> 필요한 **계산 값을 저장**해두었다가 **재사용**하는 알고리즘 설계 기법이다.

&nbsp; 큰 문제를 한번에 해결하기 어려울 때, 여러개의 작은 문제로 나누어 푸는 **'분할 정복'** 알고리즘이 있다. 이때 동일한 작은 문제들이 반복적으로 계산되는 경우가 생길 수 있다. 그 문제를 매번 재계산 하지 않고 값을 저장했다가 재사용하는 기법이 바로 다이나믹 프로그래밍이다. 메모리 공간을 약간 더 사용하여 시간을 획기적으로 줄일 수 있는 방법이다.



&nbsp; 여담이지만 다이나믹 프로그래밍의 Dynamic은 동적 할당(Dynamic Allocation)의 Dynamic과 아무런 관계가 없다.   
동적할당에서 Dynamic은 '프로그램이 실행되는 도중'에라는 의미이지만 다이나믹 프로그래밍에서 Dynamic은 고안자인 벨만(Richard E. Bellman)이 연구소에서 펀딩을 받으려고 멋있는 단어를 선택했다고 한다. Programming이란 단어는 최적화 연구 분야에서 최적의 프로그램을 찾아낸다는 의미로 사용된다.

<img src="https://user-images.githubusercontent.com/70243735/119645773-5dccc600-be59-11eb-8808-249c801fc1e2.png" width="500px">

다이나믹 프로그래밍은 다음과 같은 조건을 만족할때 사용할 수 있다.

1. **최적 부분 구조**   
    : 큰 문제를 작은 문제를 나눌 수 있다. 이러한 작은 문제의 답을 모아 큰 문제를 해결할 수 있다.

2. **중복된 하위 문제**   
    : 동일한 작은 문제를 반복적으로 해결해야 한다.

<br>

## 💡 피보나치 수열
> 다이나믹 프로그래밍으로 해결할 수 있는 대표적인 예시가 바로 피보나치 수열이다.   

피보나치 수열은 현재 항을 계산하기 위해 이전 두항의 합을 구해야한다. 이를 표현하기 위해 다음과 같은 점화식을 사용한다.

<img src="https://user-images.githubusercontent.com/70243735/119646129-c451e400-be59-11eb-8ec4-2599fa24c521.png" width="300px">

이를 재귀함수를 사용하여 코드로 구현하게 되면 다음과 같다.

```python
def fibo(x):
    if x==1 or x==2:
        return 1
    return fibo(x-1) + fibo(x-2)

print(fibo(5))
```
&nbsp; 해당 코드는 O(2^N)의 시간복잡도를 가지게 되어 N이 증가함에 따라 수행시간이 기하급수적으로 늘어난다. 예를 들어 N=30이면 약 10억 가량의 연산을 수행해야한다. f(5)일때 호출과정을 그림으로 표현하면 다음과 같다.

<img src="https://user-images.githubusercontent.com/70243735/119646340-03803500-be5a-11eb-9be4-7dd5bae9880e.png" width="500px">


그림을 통해 동일한 함수가 반복적으로 호출되는 것을 알 수 있다. 이미 한번 계산했지만 계속 호출할때마다 계산을 하는 것이다. 그림에서 fib(1)은 총 5번, fib(2)는 총 3번 호출되어 계산되었다. 다이나믹 프로그래밍은 이러한 반복적인 계산을 방지해주는 알고리즘 설계 기법이다.

<br>

## 💡 Topdown
> 탑다운 방식은 메모이제이션을 사용하여 다이나믹 프로그래밍을 구현하는 방식 중 하나이다.

&nbsp; **메모이제이션**(memoiztion)이란 한번 구한 계산 결과를 메모리 공간에 메모해두고, 같은 식을 다시 호출하면 메모한 결과 그대로 가져오는 기법을 말한다. 탑다운 방식은 큰 문제를 해결하기 위해 작은 문제를 호출한다고 하여 **하향식**이라고도 불린다. 이러한 탑다운방식은 **재귀함수**를 이용하여 구현할 수 있다.



**[ 코드: 탑다운 방식을 이용한 피보나치 수열 ]**

```python
# 한번 게산된 결과를 메모이제이션하기 위한 리스트
memo = [0]*100

# 피보나치 수열을 재귀함수로 구현(topdown)
def fibo(x):
# fibo(1)=fibo(2)=0
if x==1 or x==2:
    return 1

# 이미 계산한 적있는 문제라면 그대로 반환
if memo[x] != 0:
    return memo[x]

# 아직 계산하지 않은 문제라면 점화식에 따라서 피보나치 결과 반환
memo[x] = fibo(x-1)+fibo(x-2)
return memo[x]


print(fibo(99))
```

<br>

## 💡 Bottom-Up
> 보텀업 방식은 타블레이션(tabulation)을 사용하여 다이나믹 프로그래밍을 구현하는 방식 중 하나이다.

&nbsp; **타블레이션**(tabulation)이란 하위 문제부터 천천히 해결하면서 더 큰 문제를 해결하는 기법을 말한다. 타블레이션이라고 부르는 이유는 작은 문제부터 큰 문제까지 하나하나 테이블을 채워간다는 의미 때문이다. 보텀업 방식은 하위 문제부터 시작해서 더 큰 문제를 해결해 나가기 때문에 **상향식**이라고도 한다. 다이나믹 프로그래밍의 전형적인 형태는 바로 이 보텀업 방식이다. 보텀업방식은 **반복문**을 이용하여 구현할 수 있다.


**[ 코드: 탑다운 방식을 이용한 피보나치 수열 ]**

```python
# 작은 문제부터 해결해서 저장할 dp테이블
dp = [0]*100

# fibo(1)=fibo(2)=0
dp[1]=1
dp[2]=1
n=99

# 피보나치 수열을 반복문으로 구현(bottom up)
for i in range(3, n+1):
dp[i] = dp[i-1]+dp[i-2]

print(dp[n])
```
<br>

## 💡 다이나믹 프로그래밍 예제

### Q1. 1로 만들기
 정수 X가 주어질 때 정수 X에 사용할 수 있는 연산은 다음과 같이 4가지이다.
 
    a) X가 5로 나누어떨어지면, 5로 나눈다.

    b) X가 3으로 나누어떨어지면, 3으로 나눈다.

    c) X가 2로 나누어떨어지면, 2로 나눈다.

    d) X에서 1을 뺀다.
    
 정수 X가 주어졌을 때, 연산 4개를 적절히 사용해서 1을 만들려고 한다. 연산을 사용하는 횟수의 최솟값을 출력하시오.    
 예를 들어 정수가 26이라면 다음과 같이 계산해서 3번 연산이 최솟값이다. 
 
    1. 26-1=25
    2. 25/5=5
    3. 5/5=1

* 입력 조건

    - 첫째줄에 정수 X가 주어진다(1<=x<=30,000)   

* 출력 조건    

    - 첫째줄에 연산하는 횟수의 최솟값을 출력한다.

* 입력 예시 : 26   

* 출력 예시 : 3   

<br>

**[ 문제 아이디어 ]**

그리디 문제와 비슷해보이겠지만, 그리디 문제로 풀게되면 26이 주어졌을 때 지금 당장 선택할 수 있는 제일 좋은 방법인 c연산을 수행하였을 것이다. 때문에 이 문제는 그리디로 접근해서는 안된다.   
26이라는 숫자가 주어졌을 때, f(26)은 d연산을 수행하는 f(25), c연산을 수행하는 f(13), b연산을 수행하는 f(12)의 연산을 다시 수행하게 된다. 이를 식으로 표현하게되면 다음과 같다.   

`f(i)=min(f(i//5)+1, f(i//3)+1, f(i//2)+1, f(i)+1)`

이런식으로 큰 문제를 해결하기 위해 작은 문제들이 반복적으로 계산되는 것을 확인할 수 있다. 때문에 이 문제는 다이나믹 프로그래밍 기법을 활용했을 때 효과적으로 해결할 수 있다.

<br>

**[ 코드 ]**

```python
x = int(input())

# 작은 문제부터 해결해서 저장할 dp테이블
dp = [0]*30001

# 다이나믹 프로그래밍(bottom up)
for i in range(2, x+1):
## 연산이 가능한 모든 경우를 수행해보고 가장 작은값을 가져간다.

# d연산
dp[i] = dp[i-1]+1

# a연산이 가능한 경우
if i%5 ==0:
    dp[i] = min(dp[i], dp[i//5]+1)
# b연산이 가능한 경우
if i%3==0:
    dp[i] = min(dp[i], dp[i//3]+1)
# c연산이 가능한 경우
if i%2==0:
    dp[i] = min(dp[i], dp[i//2]+1)

print(dp[x])
```

<br>


### Q2. 개미 전사

&nbsp; 메뚜기 마을에는 여러 개의 식량창고가 있는데 식량창고는 일직선으로 이어져있다. 각 식량 창고에는 정해진 수의 식량을 저장하고 있으며 개미전사는 식량창고를 서낵적으로 약탈하여 식량을 빼앗을 예정이다. 이때 메뚜기 정찰병들은 일직선상에 존재하는 식량창고 중에서 서로 인접한 식량창고를 공격받으면 바로 알아챌 수 있다. 다라서 개미전사가 정찰병에게 들키지 않고 식량창고를 약탈하기 위해서는 최소한 한칸 이상 떨어진 식량창고를 약탈해야한다. 예를 들어 식량창고 4개가 다음과 같이 존재한다고 가정하자.   
<table>
<tr>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>5</th>
</tr>
</table>
이때 개미전사는 두번째 식량창고와 네번째 식량창고를 선택했을때 최댓값인 총 8개의 식량을 배앗을 수 있다. 개미전사는 최대한 많은 식량을 얻기 원한다. 개미전사를 위해 식량창고 N개에 대한 정보가 주어졌을때 얻을 수 있는 식량의 최댓값을 구하는 프로그램을 작성하시오.

* 입력 조건
    - 첫째줄에 식량창고의 개수 N이 주어진다.(3<=x<=100)
    - 둘째줄에 공백으로 구분되어 각 식량창고에 저장된 식량의 개수 K가 주어진다.(0<=K<=1,000)

* 출력 조건
    - 첫째줄에 개미 전사가 얻을 수 있는 식량의 최댓값을 출력하시오

* 입력예시
    ```
    4
    1 3 1 5
    ```
* 출력예시
    ```
    8
    ```

<br>

**[ 문제 아이디어 ]**

&nbsp; 현재 발견한 최대 식량이라고 막 털었다가는 최적해를 못찾을 수 있다. 때문에 이문제는 그리디로는 풀 수 없다. 현재 식량창고를 털어야 할지 안 털어야할지는 이전 식량창고에 달려있다.   
&nbsp; 예를 들어 i번째 식량창고를 털어도 괜찮은 경우는 i-1번째 식량창고를 털지 않고 i-2번째 식량창고를 털었을 경우이다. 반대로 i번째 식량창고를 털면안되는 경우는 i-1번째 식량창고를 털었을 경우이다. 그래서 i번째 식량창고를 털지안털지 결정하는 식은 다음과 같다.   

`f(i)=max(f(i-1), f(i-2)+k(i))`   

&nbsp; 이를 계산하기 위해 작은 문제들이 반복적으로 계산된다. 때문에 이 문제는 다이나믹 프로그래밍 기법을 활용했을 때 효과적으로 해결할 수 있다.

<br>

**[ 코드 ]**

```python
n = int(input())
food = list(map(int, input().split()))

# 작은 문제부터 해결해서 저장할 dp테이블
dp = [0]*100

# 다이나믹 프로그래밍(bottom up)
dp[0] = food[0]
dp[1] = max(food[0], food[1])

for i in range(n):
    dp[i]=max(dp[i-1], dp[i-2]+food[i])

print(dp[n-1])
```





<br>
<br>

출처 :   
파이썬 알고리즘 인터뷰(박상길)   
이것이 코딩테스트다(나동빈)