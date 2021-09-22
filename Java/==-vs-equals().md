# == vs equals()
> **동일성**은 **객체의 주소**를 비교하는 것이고, **동등성**은 **객체의 같음**을 비교하는 것이다. <br>
> 자바에서는 Object 클래스에 정의된 equals() 메소드가 동등성을 비교한다.

<br>

## 💡 **java에서 ==와 equals()의 차이**

- "=="
    - 항등 **연산자(Operator)** 이다.
    - 참조 비교(Reference Comparison) ; (주소 비교, Address Comparison)
        - 두 객체가 같은 메모리 공간을 가리키는지 확인한다.
    - 모든 기본 유형(Primitive Types)에 대해 적용할 수 있다.

- "equals()"
    - 객체 비교 **메서드(Method)** 이다.
    - **내용 비교(Content Comparison)**
        - 두 객체의 값이 같은지 확인한다.
        - 즉, 문자열의 데이터/내용을 기반으로 비교한다.
    - 기본 타입(Primitive Types)에 대해서는 적용할 수 없다.

<br>

## 💡 실제 equals() 분석

: String일 때는 한 글자씩 비교하지만, 아니라면 그냥 ==(참조 비교)를 사용한다. <br>
: 때문에 필요하다면 equals()를 오버라이딩해서 **동등성의 판단 기준을 정의**해주면 된다.

```java
public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        if (anObject instanceof String) {
            String anotherString = (String)anObject;
            int n = value.length;
            if (n == anotherString.value.length) {
                char v1[] = value;
                char v2[] = anotherString.value;
                int i = 0;
                while (n-- != 0) {
                    if (v1[i] != v2[i])
                        return false;
                    i++;
                }
                return true;
            }
        }
        return false;
    }
```

<br>

## 💡 "==" VS "equals()" 예시

```java
class Person {
    private String name;

    public Person(String name) {
        this.name = name;
    }

    // 동등성 비교 메소드 equals 오버라이딩
    @Override
    public boolean equals(Object object){
        Person anotherPerson = (Person) object;
        return (this.name.equals(anotherPerson.name));
    }

}

public class Main {
    public static void main(String[] args) {
        String s1 = new String("WORLD");
        String s2 = new String("WORLD");

        System.out.println("equals 비교 : " + s1.equals(s2)); // true
        System.out.println("== 비교 : " + (s1 == s2)); // false

        Person person1 = new Person("홍길동");
        Person person2 = new Person("홍길동");

        System.out.println("equals 비교 : " + person1.equals(person2));// true
        System.out.println("== 비교 : " + (person1 == person2));// false
    }
}
```