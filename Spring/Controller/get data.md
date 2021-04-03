# Controller에서 데이터 받기

&nbsp; Controller은 비지니스 로직을 처리하고 데이터를 가공한다.   이때 비지니스 로직을 처리하기위해 controller에서 데이터를 받는 방법에 대해서 알아보자.   
&nbsp; 크게 HttpServletRequest, @RequestParam, @RequestBody, @ModelAtrribute, @PathVariable이 있다.

<br>

---
다음 URL로 요청을 보낸다고 가정하자.
```
http://localhost:8080/getInfo?id=3
```
<br>

## **HttpServletRequest.getParameter()**
> 클라이언트의 요청정보를 확인하게해주는 HttpServletRequest를 이용하기
```java
@GetMapping("/getInfo");
public void getInfo(HttpServletRequest request){
    log.info("get parameter" + request.getParameter("id"));
    log.info("referer" + request.getHeader("referer")); // 이전 URL들고오기
}
```
[HttpServletRequest](./HttpServletRequest.md)는 파라미터를 가져오는 것외에도 현재나 이전의 URL을 들고오는 일 등을 할 수 있다.

<br>

## **@RequestParam**
> 파라미터를 1:1로 받기
```java
@GetMapping("/getInfo");
public void getInfo(@RequestParam(value="id", required="false", defaultValue="mangdo")String id){
    log.info("get parameter" + id);
}
```

**required**는 파라미터의 필수 여부이다. 디폴트값은 true이다.  
**defaultVaule**로 required="false"면서 만약 해당 파라미터를 받지않았다면 파라미터의 기본값을 설정해줄 수 있다.  

만약 requried="true"면서 파라미터가 넘어오지않게되면 400에러가 발생한다. 

<br>

## **@ModelAttribute**
> 파라미터를 객체로 받기 ( JavaObject로 매핑 )
```java
@GetMapping("/getInfo");
public void getInfo(@ModelAttribute("user") UserVO user){
    log.info("get parameter" + user.getId());
}
```

@RequestParam과 비슷한 방법이지만, 파라미터를 1:1로 하나씩 받는게 아닌 **여러 파라미터들을 받아서 자바의 객체로 매핑**한다. (객체로 한번에 바인딩해서 받는다.) 때문에 변수들이 Setter함수가 없다면 저장되지않는다.

<br>

## **어노테이션 생략시?**
> String, Long타입은 @RequestParam으로 취급하고 이외에는 @ModelAttribute로 취급한다.

어노테이션을 생략하고 간단하게 받을 수도 있다. 대신 이경우에는 변수명과 동일한 파라미터값만 받을 수 있다.
```java
@PostMapping("/getInfo");
public void getInfo(String id, UserVO user){
    log.info("get parameter" + id);
    log.info("get parameter" + user.getId());
}
```

<br>

## **@RequestBody**
> 파라미터를 객체로 받기 ( **MessageConver**를 사용하여 javaObject로 변환 )

```java
@PosMapping("/getInfo");
public void getInfo(@RequestBody UserVO user){
    log.info("get parameter" + user.getId());
}
```

@ModelAttribute와 마찬가지로 파라미터를 객체로 받는다. 하지만 @ModelAttribute와 다른점은 **MessageConverter를 이용해서 자바의 객체로 변환**한다는 점이다.   
때문에 다음과 같은 특징을 가진다.

1. **POST**요청과 함께 사용되어야한다.

 : MessageConverter는 HTTP 요청의 Body내용을 자바의 객체로 변환시킨다. GET방식의 메소드는 애초에 Body가 존재하지 않기때문에 에러를 발생시킨다.

2. **JSON 데이터받을 때 주로 사용**

 : JSON이나 XML과 같은 데이터를 MessageConverter를 이용해서 자바의 객체로 변환한다. 

3. Setter가 없어도 된다.

 : @ModelAttribute는 자바의 객체로 1:1 매핑이기에 Setter가 필수지만 @RequestBody는 MessageConverter를 통한 자바의 객체로 변환이기때문에 Setter가 없어도 괜찮다.

<br>

## **@PathVariable**
> URL 정의 부분과 메소드 내에 파라미터에 정의하여 사용

단, null이나 공백값이 들어가는 파라미터라면 적용하지 말아야한다. 값에 마침표(.)가 있다면 마침표 뒤가 잘려서 나온다.
요청 URL은 다음과 같다.

```
http://localhost:8080/getInfo/3
```

```java
@PosMapping("/getInfo/{id}");
public void getInfo(@PathVariable String id){
    log.info("get parameter" + id);
}
```
만약 변수명을 다르게 사용하고 싶다면 다음과 같이 명시를 해줘야 한다.
```java
@PosMapping("/getInfo/{id}");
public void getInfo(@PathVariable("id") String userId){
    log.info("get parameter" + userId);
}
```