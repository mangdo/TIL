# 빌더 패턴
> 객체의 생성 과정과 표현 방법을 분리하여 <br>
동일한 생성 절차에서 서로 다른 표현 결과를 만들 수 있게 하는 패턴

<br>

## 💡 빌더 패턴의 장점

- 매개변수의 순서를 기억하지 않아도 된다<br>
    → 매개변수가 많은 객체를 생성할 때 도움 된다.
    
- 가독성이 좋아진다<br>
    → User.builder().name("minseo").age(20).build();<br>
    → name이 민서다. age가 15다.<br>
    
- 생성자를 여러 개 만들 필요가 없다<br>
     → 생성할 객체의 종류를 손쉽게 추가, 확장이 가능한 설계<br>
     → 유연성이 좋아진다.<br>

## 💡 빌더 패턴 예제 코드

- User객체

```java
public class User {
    // 이름
    private String name;

    // 나이
    private int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

		// 빌더 
    public static UserBuilder builder() {
        return new UserBuilder();
    }

    public static class UserBuilder {
        private String name;
        private int age;

        // 모든 필드가 디폴트값으로 설정됨
        UserBuilder() {}

        public UserBuilder name(String name) {
            this.name = name;
            return this;
        }

        public UserBuilder age(int age) {
            this.age = age;
            return this;
        }

        public User build() {
            return new User(name, age);
        }
    }
}
```

- User객체를 빌더 패턴 이용하여 생성

```java
public void test() {
	User user = User.builder()
            .age(20)
            .name("minseo")
            .build();

	User user2 = User.builder()
                .name("minseo")
                .build(); // age는 0으로 생성
}
```

- 롬복 사용

: 롬복을 사용하면 빌더 패턴을 간단하게 구현할 수 있다,

```java
public class User {

    // 이름
    private String name;

    // 나이
    private int age;

    @Builder
    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```
