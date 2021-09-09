# 배열(Array)

> 배열은 **같은 종류**의 데이터를 **순차적으로 저장**하는 데이터 구조이다.

<br>

## 💡 배열의 장점과 단점

- 장점 <br>
    : **인덱스**를 통한 빠른 접근 가능

- 단점 <br>
    : 데이터 추가/삭제가 쉽지 않다. <br>
    : 배열 객체를 선언하는 동안 배열의 길이를 정의해야한다. <br>
    : 한번 정의된 **배열의 길이는 변경할 수 없다**.

<br>

## 💡 자바에서의 배열

```java
public class Main {
    public static void main(String[] args) {

        // 배열 선언
        int[] numbers1 = new int[5];

        // 배열 초기화
        for (int i = 0; i < numbers1.length; i++) {
            numbers1[i] = i;
        }

        // 배열 선언 및 초기화
        int[] numbers2 = {0, 1, 2, 3, 4};
        String[] weeks = {"월", "화", "수", "목", "금", "토", "일"};

        // 배열에 요소 추가
        // numbers2[5] = 5; ArrayIndewOutOfBoundsException 에러발생

        // 새로운 더 큰 배열을 만든다.
        numbers2 = Arrays.copyOf(numbers2, numbers2.length + 1);
        // 배열에 요소 추가
        numbers2[5] = 5;

        // 결과 출력
        System.out.println("배열에 요소 추가: " + Arrays.toString(numbers2));
    }
}

```

#### ✋ 막간 JAVA 공부!
* Arrays.copyOf() <br>
    : 특정 배열의 원하는 길이만큼 새로운 배열로 복사하는 함수 <br>
    ```java
        int[] arr = {1, 2, 3, 4, 5};
        // 기존 배열을 복사해서 새로운 배열을 만든다.
        int[] arr1 = Arrays.copyOf(arr, 2);
        int[] arr2 = Arrays.copyOf(arr, 7);

        // 결과 출력
        System.out.println("크기가 2인 배열로 새로 만들기: " + Arrays.toString(arr1));
        // [1, 2]
        System.out.println("크기가 7인 배열로 새로 만들기: " + Arrays.toString(arr2));
        // [1, 2, 3, 4, 5, 0, 0]
    ```
<br>

## 💡 파이썬의 배열
: 파이썬에서는 리스트 타입이 배열기능을 제공하고 있다. <br>
파이썬의 리스트는 원래 배열보다는 다양한 기능을 제공하고 있다. 때문에 배열의 단점이 와닿지 않을 수 있다.

```python
# 배열 선언 및 초기화
data = [1,2,3,4,5]

# 배열 요소 추가
data.append(1)
print(data)
# [1,2,3,4,5,1]

data = data + [2]
print(data)
# [1,2,3,4,5,1,2]

```