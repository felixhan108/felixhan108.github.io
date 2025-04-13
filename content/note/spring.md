---
title: Spring Boot 실무 GUIDE
version: 0.0.2
latestUpdate: 2025-04-08
description: 개인 프로젝트에서는 flask나 express.js 를 이용하지만 레거시 프로젝트의 소스를 보게 되거나 진행하게 될 경우 SpringBoot를 알아야 합니다. 실무에서의 사용을 위해 속성으로 '애플코딩'의 수업을 듣고 springboot+jpa의 flow를 작성 해 보았습니다.
---

## 설치방법

1. http://start.spring.io/ 에 접속해 셋팅이 완료된 프로젝트를 얻는다.
2. Gradle, Spring Boot 3.x, Java17이나 21버전으로 다운로드 받는다.
3. 에디터의 SDK 버전을 Java와 동일하게 맞춥니다.

## 프로젝트 폴더 설명

- src : 실제 코드 위치
- resources : html,css,js,image 등 asset의 역활
- application.properties : 환경변수 또는 프로젝트 설정 보관
- build.gradle : 프로젝트 이름, 버전, 라이브러리 기록용 파일

## java 프로젝트의 시작 코드

```java
public static void main(String[] args) {
	SpringApplication.run(ShopApplication.class, args);
}
```

## java 의 키워드

- var
- final : 재 할당 불가능한 변수
- public : 클래스에 변수랑 함수 만들때 export 하는 개념
- package private : export를 안한 경우 'public'을 안쓴 경우
- private : 다른클래스에서 사용 금지
  - getter, setter
- protected : 같은 폴더 클래스에선 사용 가능하나 다른 폴더로 가면 사용 불가 (extends 시 사용 가능 )
- static : new 없이 다른곳에서 사용 가능 (유틸리티 같은 성격으로 사용 하기도 함)

```java
// 간단한 Getter,Setter 개념
@Getter
@Setter
public class Test {
	private Integer age;
	private String name;
	public void addAge() {
		this.age = this.age + 1;
	}
	public void ageSetting(Integer a){
		// ageSetting 중 100살이 넘어가면 삽입할 수 없도록 하는 경우
		if(a > 0 && a < 100) {
			this.age = a;
		}
	}
}

// 사용 예
var a = new Test();
a.setName("한성수"); // Setter를 사용
a.setAge("20"); // Setter를 사용
a.ageSetting("34");
a.addAge();
```

## class 문법

```java
// class 생성
class Test {
	String name = "Han"; // 변수 / filed / attribute
	void hello(){ System.out.println("hi"); } // function / method
}

// class 사용
Test test new Test();
// class에서 뽑아온 new Test() 는 Object/인스턴스 라 부른다.
```

## constructor 문법

```java
class Friend {
	String name = "kim";
	int age = 20;
	Friend(String name){
		this.name = name // constructor
	}
}

// 사용시
var friend1 = New Friend("han");
var friend2 = New Friend("kim");
```

## Controller 만들기

```java
// BasicContoller.java
package com.apple.shop;

@Controller
public class BasicController {
	@GetMapping("/") // 해당 경로 방문시
	@ResponseBody // body 값이 응답 됨.
	String Hello(){
		return "sending data for User" // html 이나 html 파일도 전달이 가능.
	}
}
```

## Thymeleaf

서버 데이터를 html에 넣어주는 외부 라이브러리

```java
@Controller
public class ListController {
	@GetMapping("/list")
	String list(Model model) {
		model.addAtrribute("name", "한성수");
		return "list.html";
	}
}
```

```html
<!-- list.html -->
<h4 th:text="${name}">바지</h4>
```

## Database 호스팅 받기

Azure, AWS, Supabase 등 DB 서비스를 받아야 하며 사용 방법 또는 해당 서비스들의 정책은 따로 정리를 해둘 것.

## DB 데이터 생성과 출력

_JPA, Lombock 라이브러리가 사용 되었습니다._

### 테이블 만들기 (@Entity)

```java
// Item.java
@Entity
public class Item {
	// primary key, auto Increment
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;

	@Column(length = 200) // 최대길이를 지정해 200자가 넘어가면 db 저장 실패
	@Column(nullable = false) // 컬럼에 데이터가 비어있을 경우 저장 실패
	@Column(unique = true) // 동일 정보가 들어오면 저장 실패
	@Column(columnDefinition = "TEXT") // 매우 긴 문자 저장시 적용
	private String title;
	private Integer price;
}
```

### Repository 생성

```java
public interface ItemRepository extends JpaRepository<Item, Long> {
}
```

### Controller에 Repository 등록

```java
@Controller
@RequiredArgsConstructor // Lombok lib
public class ItemController {
	private final ItemRepository itemRepository;

	// dependecny injection
	@Auotowired
	ItemController(ItemRepository itemRepository){
		this.itemRepository = itemRepository;
	}
}
```

### DB 입출력 문법

```java
// ItemController.java

@GetMapping("/list")
String list(Model model){
	List<Item> result = itemRepository.findAll(); // DB 출력
	model.addAttribute("Items", result);

	return "list.html"
}
```

## [통합] '상품 추가 기능' 만들어보기

### 1.글 작성 페이지

```html
<form action="/add" method="POST">
  <input name="title" />
  <input name="price" />
  <button type="button">Sned</button>
</form>
```

### 2.글 작성 페이지로 이동하는 컨트롤러

```java
@GetMapping("/write");
String write() {
	return "write.html";
}
```

### 3.보내기 버튼 클릭 시 이동하는 컨트롤러

```java
@PostMapping("/add");
String writePost(@RequestParam String title, @RequestParam  Integer price) {
	Item item = new Item;
	item.setTitle(title);
	item.setPrice(price);
	itemRepository.save(item);

	return "redirect:/list";
}
```

#### 3-1.유저가 보낸 데이터를 Object로 바로 변환하고 싶으면?

```java
@PostMapping("/add");
String writePost(@ModelAttribute Item item) {
	// @ModelAttribute 사용시 var 변수명 = new 클래스명() 알아서 해주고 유저가 보낸 데이터를 다 집어넣어 줌
	itemRepository.save(item);
	return "redirect:/list";
}
```

## URL 파라미터

```java
@GetMapping("/detail/{id}")
String detail(){
	return "detail.html";
}
```

## DB에서 글을 뽑아 html에 적용

```java
@GetMapping("/detail/{id}")
String detail(@PathVariable Long id, Model model){ // @PathVariable Long id = 유저가 입력한 param을 가져옴
	Optional<Item> result = itemRepository.findById(1L); // id가 1인 행을 찾아 옴.

	if (result.isPresent()){
		model.addAttribute("data", result.get()); // 가져온 데이터를 Detail.html에 꽂음.
		return "detail.html";
	} else {
		return "redirect:/list";
	}
}
```

## REST API의 예외처리 방법

### try catch

```java
@GetMapping("/detail/{id}")
@ResponseBody
String detail() {
	try {
		throw new Exception("error...error..."); // 에러를 강제로 발생 시킴
	} catch (Exception e){
		return "error !!!"
	}
}
```

### thorws Exception

```java
@GetMapping("/detail/{id}")
@ResponseBody
String detail() thorws Exception {
	thorw new Exception("error...");
}
```

### ResponseEntity

```java
@GetMapping("/detail/{id}")
ResponseEntity<String> detail() { // REST API 생성시 error 별 code 전달
	try{
		throw new Exception("errorr...");
	} catch(Exception e) {
		return ResponseEntity.status(400).body("reason error");
	}
}
```

### @ExceptionHandler

try catch 대신 spring boot가 제공해주는 예외 처리 기능

```java
@ExceptionHandler(Exception.calss)
public ResponseEntity<String> exceptionHandler() {
	return ResponseEntity.status().body("");
}
```

### @ControllerAdvice

전체 컨트롤 클래스에 대한 error를 정하는 방법

```java
@ControllerAdvice
public class MyExceptionHandler {
	@ExceptionHandler(Exception.class)
	public ResponseEntity<String> handler() {
		return ResponseEntity.status(400).body("모든 컨트롤러 에러시 발동");
	}
}
```

### 특정에러만 실행

```java
@ControllerAdvice
public class MyExceptionHandler {
	@ExceptionHandler(MethodArgumentTypeMismatchException.class)
	public ResponseEntity<String> handler() {
		return ResponseEntity.status(400).body("특정 에러시 발동");  
	}
}
```

## 'Service' 레이어의 분리

백엔드의 MVC패턴 (Model, View, Controller)를 아래와 같이 나눌 수 있다.
Repository - 백엔드의 DB (DTO)
Service - 백엔드의 비지니스로직
Controller - 백엔드의 router

```java
@Service
@RequiredArgsConstructor
public class ItemService {
	private final ItemRepository itemRepository;

	public void saveItem(){
		Item item = new Item();
		item.setTitle(title);
		item.setPrice(price);
		itemRepository.save(item);
	}
}
```

## 수정기능

```java
@GetMapping("/edit/{id}")
String edit(Model model) {
  Optional<Item> result = itemRepository.findById(1L);
  if (result.isPresent()) {
    model.addAttribute("data", result.get());
    return "edit.html";
  } else {
    return "redirect:/list";
  }
}
```
