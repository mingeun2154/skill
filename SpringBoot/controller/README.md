# Controller

> ### references 🔗
> 초보 웹 개발자를 위한 스프링5    
> https://mangkyu.tistory.com/49    
> https://www.baeldung.com/spring-request-response-body     

## Contents		
* ### [MVC 컨트롤러](https://github.com/mingeun2154/skill/tree/main/SpringBoot/controller#spring-mvc-controller)
* ### [@Controller vs @RestController](https://github.com/mingeun2154/skill/tree/main/SpringBoot/controller#controller-vs-restcontroller-1)      

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
