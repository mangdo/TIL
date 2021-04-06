# RestController

&nbsp; Spring에서 컨트롤러를 등록하는 방법에는 두가지가 있다. 바로 @Controller와 @RestController이다. @Controller는 주로 View를 반환한다. @Controller에 [@ResponseBody](./return%20data.md)를 붙이면 view가 아닌 xml, json과 같은 데이터를 반환할 수 있다.

매번 @ResponseBody를 붙이는 것은 번거로우니 Spring 4.0부터는 @RestController를 지원하기 시작했다.

## **@RestController**
> @Controller + @ResponseBody

<img src="https://user-images.githubusercontent.com/70243735/113699225-3dfa0b00-9710-11eb-907d-81a473dee440.PNG" width="450px">

&nbsp; 실제 @RestController를 확인해보면 위의 사진과 같다. @RestController는 Spring 4.0.1 부터 사용가능한 어노테이션으로 @Controller에 @ResponseBody가 결합된 어노테이션이다.  @RestController의 모든 메소드에서 리턴되는 값은 MessageConverter에서 변환되어 HTTP Response Body에 쓰여진다.

* 기존의 @Controller를 사용하는 코드
    ```java

    @Controller
    public class SampleController{
        @GetMapping("/example")
        @ResponseBody
        public SampleDTO example() {
    
            SampleDTO dto = new SampleDTO();
            dto.setAge(24);
            dto.setName("mangdo");
        
            return dto;
        }
    }
    ```
* @RestController를 사용하는 코드로 수정
    ```java
    @RestController
    public class SampleController{

        @GetMapping("/example")
        public SampleDTO example() {
        
            SampleDTO dto = new SampleDTO();
            dto.setAge(24);
            dto.setName("mangdo");
            
            return dto;
        }
    }
    ```

<br>

## **@RestController 사용예시**

1. 텍스트 컨텐츠를 반환

    ```java
    @RequestMapping("/rest") 
    public String rest1() { 
        return "text content"; 
    }
    ```

2. 컨텐츠 형식을 지정한다.

    &nbsp; **consumes**는 받는 컨텐츠 형식이고, **produces**는 응답하는 컨텐츠 형식이다. org.springframework.http.MediaType 클래스에 콘텐츠 형식의 상수가 정의되어 있으니 이것을 이용하는 것이 좋다.

    ```java
	@PostMapping(value="/new", consumes="application/json", produces= {MediaType.TEXT_PLAIN_VALUE})
	public ResponseEntity<String> create(@RequestBody ProductReviewVO vo){
		log.info("ReviewVO : " + vo);

		return service.register(vo)==1?
				new ResponseEntity<>("success",HttpStatus.OK) :
				new ResponseEntity<>(HttpStatus.INTERNAL_SERVER_ERROR);
		
	}
    ```
 

3. HTTP 상태 및 응답헤더를 지정해준다.

    &nbsp; HTTP 상태와 같은 컨텐츠 형식 이외의 응답 헤더를 지정해주고 싶다면 반환값을 ResponseEntity로 한다.

    ```java
	@PostMapping(value="/new", consumes="application/json", produces= {MediaType.TEXT_PLAIN_VALUE})
	public ResponseEntity<String> create(@RequestBody ProductReviewVO vo){
		log.info("ReviewVO : " + vo);

		return service.register(vo)==1?
            new ResponseEntity<>("success",HttpStatus.OK) :
		    new ResponseEntity<>(HttpStatus.INTERNAL_SERVER_ERROR);
		
	}
    ```

4. JSON 반환

    &nbsp; 반환값을 임의의 클래스라면 springMVC가 Jackson을 사용하여 json으로 변경하여 반환해준다.

    ```java
	@GetMapping("/quickView")
	public ProductVO getQuickView(Long product_id) {
		
		log.info("quick View data, " + product_id);
		
        return service.getQuickView(product_id);
	}
    ```
