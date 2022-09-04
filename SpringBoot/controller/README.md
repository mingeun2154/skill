# Controller

> ### references 🔗
> 초보 웹 개발자를 위한 스프링5    
> Reac.js, 스프링 부트, AWS로 배우는 웹 개발 101   
> https://www.baeldung.com/spring-request-response-body     

## Contents		
* ### [MVC 컨트롤러](https://github.com/mingeun2154/skill/tree/main/SpringBoot/controller#spring-mvc-controller)
* ### [@Controller vs @RestController](https://github.com/mingeun2154/skill/tree/main/SpringBoot/controller#controller-vs-restcontroller-1)      
* ### [데이터를 포함하는 요청](https://github.com/mingeun2154/skill/tree/main/SpringBoot/controller#request-with-data)
* ### [객체를 포함하는 응답](https://github.com/mingeun2154/skill/tree/main/SpringBoot/controller#@responsebody)

#    

## Spring MVC Controller
웹 요청을 처리하고 그 **결과를 view에 전달**하는 스프링 bean이다.

스프링 컨트롤러로 사용될 클래스는 @Controller 애노테이션을 붙여야 하고, @GetMapping, @PostMapping 요청 매핑 애노테이션으로 처리할 경로를 지정한다.

## @Controller vs @RestController

### @Controller
@Controller는 주로 **view에 값을 전달하고 view를 반환**하기 위해 사용한다.

@ResponseBody 애노테이션을 사용하면 view가 아닌 data를 반환할 수 있다. 이 애노테이션이 붙은 컨트롤러가 리턴하는 객체는 자동으로 **JSON으로 직렬화되어 HttpResponse 객체로 전달**된다.

### @RestController
스프링4 버전부터 @RestController 애노테이션이 추가되면서 @ResponseBody 애노테이션을 쓸 필요가 없어졌다.

스프링 4.3부터 @GetMapping, @PostMapping, @PutMapping, @DeleteMapping이 지원된다.

```Java
@Controller
public class RestMemberController {
	private MemberDao memberDao;
	private MemberRegisterService registerService;

	@RequestMapping(path="/api/members", method=RequestMethod.GET)
	@ResponseBody // 이 메서드가 리턴하는 값은 JSON으로 변환되어 클라이언트로 전송된다.
	public List<Member> members() {
		return memberDao.selectAll();
	}
}
```

> @Controller, @ResponseBody 애노테이션 사용

```Java
@RestController
public class RestMemberController {
	private MemberDao memberDao;
	private MemberRegisterService registerService;

	@GetMapping("/api/members")
	public List<Member> members(){
		return memberDao.selectAll();
	}
}
```

> @RestController 애노테이션 사용  

## Request with data

* [@PathVariable](#) : **경로의 일부를 argument로 인식한다.**

* [@RequestParam](#) : 매개변수를 통해 값을 전달.

* [@RequestBody](#) : 객체를 전달.

### @PathVariable and @RequestParam

```Java
@RestController
@RequestMapping("/test")
public class TestController {
	
	@GetMapping
	public String testController() {
		return "hello test";
	}

	@GetMapping("/{id}")
	public String testControllerWithPathVariable(@PathVariable(required = false) int id){
		return "path variable : " + id;
	}

	@GetMapping		// 오류 발생. 첫 번째 메서드와 경로가 겹친다.
	public String testControllerWithRequestParam(@RequestParam(required = false) int id) {
		return "request parameter : " + id;
	}
}
```

마지막 컨트롤러를 추가하면 아래와 같은 오류 메세지가 출력되며 프로세스가 종료된다.

java.lang.IllegalStateException: Ambiguous mapping. Cannot map 'testController' method

첫 번째와 세 번째 메서드의 매핑 경로가 겹치기 때문이다.

사실 두 번째 메서드도 `required = false`이기 때문에 매개변수를 전달하지 않으면 경로가 겹치게 된다. 하지만 이 경우에는 첫 번째 메서드가 실행되었다.

### @RequestBody
전달하고자 하는 리소스가 **복잡**할때 사용한다. 예를 들어 String, int같은 기본 자료형이 아니라 **객체**처럼 복잡한 자료형을 통째로 요청에 보내고 싶을 때 사용한다.

이 때 데이터는 **DTO**라는 객체에 저장되어 전달된다. 

```Java
@Data
public class TestRequestBodyDTO {
	private int id;
	private String message;
}
```	

> `@Data`는 `@Getter`, `@Setter`, `@RequiredArgsConstructor`, `@ToString`, `@EqualsAndHashCode`를 한 번에 설정해주는 lombok 애노테이션이다.

```Java
@PostMapping("/testRequestBody")
public String testRequestBody(@RequestBody TestRequestBodyDTO testRequestBodyDTO) {
	return "id : " + testRequestBody.getId() + "\nmessage : " + testRequestBody.getMessage()";
}
```

`@RequestBody TestRequestBodyDTO testRequestBodyDTO` : RequestBody로 전달되는 JSON을 TestRequestBodyDTO 객체로 변환해 가져온다.

## @ResponseBody

요청에 대한 응답으로 객체를 반환할 수 있다. `@RestController`는 `@Component`와 `@ResponseBody`의 조합으로 이루어져 있다.

`@ResponseBody` 애노테이션이 붙은 메서드가 반환한 객체는 스프링에 의해 JSON 형태로 변환되고 HttpResponse 객체에 담겨 반환된다.
