# Controller에서 데이터 전달하기

&nbsp; Controller에서 비지니스 로직을 수행하고 처리한 데이터를 View에 넘겨 페이지에 표시한다.
이때 Controller에서 View로 데이터를 전달하는 방법에는 model(modelMap)과 modelAndView이 있다.

<br>

-----

## **1. Model**

> **데이터만** 저장한다.

Model은 파라미터 방식으로 넣어주고, String 형태로 View이름을 리턴한다.  
**model.addAttribute("key","value"**)로 데이터 넣고 View에서 그 데이터를 사용한다.   
View페이지에서 ${key}이런식으로 데이터를 사용한다.
```java
@RequestMapping("/")
public String toMainPage(Model model){

  model.addAttribute("recentList", productService.getRecentList());
  model.addAttribute("saleList", productService.getSaleList());
  model.addAttribute("popularList", productService.getPopularList());

  return "/mainPage";
}
```
<br>

## **1-2. ModelMap**
> Model의 구현체

Model은 인터페이스이고 ModelMap은 Model의 구현클래스이다. 활용상의 차이는 없다.
```java
@RequestMapping("/")
public String toMainPage(ModelMap modelMap){

  modelMap.addAttribute("recentList", productService.getRecentList());
  modelMap.addAttribute("saleList", productService.getSaleList());
  modelMap.addAttribute("popularList", productService.getPopularList());

  return "/mainPage";
} 
```
<br>

## **2. ModelAndView**
> **데이터와 이동하고자하는 View페이지**를 저장한다.

Model은 인터페이스였지만 ModelAndView는 클래스이다.   
컴포넌트방식(객체 방식)으로 생성하고 리턴한다.   
마찬가지로 View에서 ${key}로 사용하면된다.

* **modelAndView.addObject("key","value"**)    
: 데이터 저장   
* **modelAndView.setView("뷰이름"**)    
: 이동하고자하는 뷰를 저장한다.   
: URL도 이동, 화면도 이동하게된다. request가 이어지지않는다.   
* modelAndView.setViewName("뷰이름")    
: 이동하고자하는 뷰를 저장한다.
: URL의 변화는 없고 화면만 변화한다. request가 이어진다. 주로 validation에 이용된다.


```java
@RequestMapping("/")
public String toMainPage(){

	ModelAndView mav = new ModelAndView();
 	
    mav.addObject("recentList", productService.getRecentList());
 	mav.addObject("saleList", productService.getSaleList());
	mav.addOjbect("popularList", productService.getPopularList());
	
    mav.setView("/mainPage");
    
	return mav;
}
```

&nbsp; ModelAndView는 @controller가 있기 전부터도 있었다. @Controller 이전에는 ModelAndView를 통해서 뷰페이지를 전달했지만 @Controller이후에는 주로 Model, ModelMap을 사용한다.