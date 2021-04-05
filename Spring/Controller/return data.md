# Controller에서 데이터 반환하기

&nbsp; 전통적인 Spring MVC의 컨트롤러인 @Controller는 주로 View를 반환한다. 하지만 @Controller에서 View가 아닌 데이터(JSON이나 XML)를 반환시킬 수도 있다. @Controller에서 데이터를 반환시키는 방법에는 @Responsebody와 ResponseEntity<>가 있다.

* View를 반환하는 Controller

    <img src ="https://user-images.githubusercontent.com/70243735/113568185-037a6a80-964b-11eb-9211-b950904b43bc.PNG" width="450px">

<br>

## **1. @ResponseBody**
> @Controller에서 JSON이나 XML같은 데이터를 반환


<img src="https://user-images.githubusercontent.com/70243735/113568428-81d70c80-964b-11eb-97fa-9a64e91ea817.PNG" width="450px">

&nbsp; @ResponseBody를 사용한 메소드에서 리턴되는 값은 **MessageConverter에서 변환되어 HTTP Response Body에 쓰여진다.** MessageConverter에는 다양한 종류가 있는데 메소드에서 리턴되는 데이터 타입에 따라 MessageConverter가 결정된다.

<details>
<summary>MessageConverter의 종류</summary>
[ 디폴트 ]

* ByteArrayHttpMessageConverter
* StringHttpMessageConverter
* FormHttpMessageConverter
* SourceHttpMessageConverter

[ 그 외 ]

: 디폴트를 제외한 이들은 직접 AnnotationMethodHanlderAdapter의 messageConverters에 등록하고 사용해야 했다. 하지만 spring 3.1이후에서는 <annotation-driven />을 사용함으로써 자동 등록이 된다.

* Jaxb2RootElementHttpMessageConverter
* MashallingHttpMessageConverter
* MappingJacksonHttpMessageConverter    
    : Jackson의 ObjectMapper를 이용해서 JSON과 오브젝트 사이의 변환을 지원

</details>

<br>

* 객체로 반환
    ```java
    @GetMapping("/example")
    @ResponseBody
    public SampleDTO example() {
        SampleDTO dto = new SampleDTO();
        
        dto.setAge(24);
        dto.setName("mangdo");

        return dto; 
        //스프링이 자동으로 JSON타입으로 객체를 반환해서 전달한다.
    }
    ```
* HashMap으로 반환

    ```java
    @GetMapping("/example")
    @ResponseBody
    public HashMap<String, Object> example() {
        HashMap<String,Object> map = new HashMap<String,Object>();
        
        map.put("age", 24);
        map.put("name", "mangdo");
        
        return HaspMap; 
        //스프링이 자동으로 JSON타입으로 반환해서 전달한다.
    }
    ```

<br>

## **2. ResponseEntity<>**
> HTTP 헤더에 Content-Type 을 명시하면서 다른 작업도 해주고 싶을때

&nbsp; Spring 어노테이션이 아닌 직접 HTTP 헤더를 다루는 경우이다. @ResponseBody보다 번거롭지만 보다 추가적인 작업을 할 수 있다. 데이터타입을 JSON으로 사용했다는 것을 알려주려면 HTTP 헤더에 contents-type을 명시해야한다.


```java
@GetMapping("/example")
public ResponseEntity<String> example(){
    // msg = {"name" : "홍길동"}
    String msg = "{ \" name \": \" 홍길동 \" }";

    HttpHeaders header = new HttpHeaders();
    header.add("Content-Type", "application/json; charset=UTF-8");

    return new ResponseEntity<>(msg,header,HttpStatus.OK);
}
```


<br>

참고 출처 :   
highcode.tistory.com/24  
joont92.github.io/spring/MessageConverter/