# Controller

> ### references ๐
> ์ด๋ณด ์น ๊ฐ๋ฐ์๋ฅผ ์ํ ์คํ๋ง5    
> Reac.js, ์คํ๋ง ๋ถํธ, AWS๋ก ๋ฐฐ์ฐ๋ ์น ๊ฐ๋ฐ 101   
> https://www.baeldung.com/spring-request-response-body     

## Contents		
* ### [MVC ์ปจํธ๋กค๋ฌ](https://github.com/mingeun2154/skill/tree/main/SpringBoot/controller#spring-mvc-controller)
* ### [@Controller vs @RestController](https://github.com/mingeun2154/skill/tree/main/SpringBoot/controller#controller-vs-restcontroller-1)      
* ### [๋ฐ์ดํฐ๋ฅผ ํฌํจํ๋ ์์ฒญ](https://github.com/mingeun2154/skill/tree/main/SpringBoot/controller#request-with-data)
* ### [๊ฐ์ฒด๋ฅผ ํฌํจํ๋ ์๋ต](https://github.com/mingeun2154/skill/tree/main/SpringBoot/controller#@responsebody)

#    

## Spring MVC Controller
์น ์์ฒญ์ ์ฒ๋ฆฌํ๊ณ  ๊ทธ **๊ฒฐ๊ณผ๋ฅผ view์ ์ ๋ฌ**ํ๋ ์คํ๋ง bean์ด๋ค.

์คํ๋ง ์ปจํธ๋กค๋ฌ๋ก ์ฌ์ฉ๋  ํด๋์ค๋ @Controller ์ ๋ธํ์ด์์ ๋ถ์ฌ์ผ ํ๊ณ , @GetMapping, @PostMapping ์์ฒญ ๋งคํ ์ ๋ธํ์ด์์ผ๋ก ์ฒ๋ฆฌํ  ๊ฒฝ๋ก๋ฅผ ์ง์ ํ๋ค.

## @Controller vs @RestController

### @Controller
@Controller๋ ์ฃผ๋ก **view์ ๊ฐ์ ์ ๋ฌํ๊ณ  view๋ฅผ ๋ฐํ**ํ๊ธฐ ์ํด ์ฌ์ฉํ๋ค.

@ResponseBody ์ ๋ธํ์ด์์ ์ฌ์ฉํ๋ฉด view๊ฐ ์๋ data๋ฅผ ๋ฐํํ  ์ ์๋ค. ์ด ์ ๋ธํ์ด์์ด ๋ถ์ ์ปจํธ๋กค๋ฌ๊ฐ ๋ฆฌํดํ๋ ๊ฐ์ฒด๋ ์๋์ผ๋ก **JSON์ผ๋ก ์ง๋ ฌํ๋์ด HttpResponse ๊ฐ์ฒด๋ก ์ ๋ฌ**๋๋ค.

### @RestController
์คํ๋ง4 ๋ฒ์ ๋ถํฐ @RestController ์ ๋ธํ์ด์์ด ์ถ๊ฐ๋๋ฉด์ @ResponseBody ์ ๋ธํ์ด์์ ์ธ ํ์๊ฐ ์์ด์ก๋ค.

์คํ๋ง 4.3๋ถํฐ @GetMapping, @PostMapping, @PutMapping, @DeleteMapping์ด ์ง์๋๋ค.

```Java
@Controller
public class RestMemberController {
	private MemberDao memberDao;
	private MemberRegisterService registerService;

	@RequestMapping(path="/api/members", method=RequestMethod.GET)
	@ResponseBody // ์ด ๋ฉ์๋๊ฐ ๋ฆฌํดํ๋ ๊ฐ์ JSON์ผ๋ก ๋ณํ๋์ด ํด๋ผ์ด์ธํธ๋ก ์ ์ก๋๋ค.
	public List<Member> members() {
		return memberDao.selectAll();
	}
}
```

> @Controller, @ResponseBody ์ ๋ธํ์ด์ ์ฌ์ฉ

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

> @RestController ์ ๋ธํ์ด์ ์ฌ์ฉ  

## Request with data

* [@PathVariable](#) : **๊ฒฝ๋ก์ ์ผ๋ถ๋ฅผ argument๋ก ์ธ์ํ๋ค.**

* [@RequestParam](#) : ๋งค๊ฐ๋ณ์๋ฅผ ํตํด ๊ฐ์ ์ ๋ฌ.

* [@RequestBody](#) : ๊ฐ์ฒด๋ฅผ ์ ๋ฌ.

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

	@GetMapping		// ์ค๋ฅ ๋ฐ์. ์ฒซ ๋ฒ์งธ ๋ฉ์๋์ ๊ฒฝ๋ก๊ฐ ๊ฒน์น๋ค.
	public String testControllerWithRequestParam(@RequestParam(required = false) int id) {
		return "request parameter : " + id;
	}
}
```

๋ง์ง๋ง ์ปจํธ๋กค๋ฌ๋ฅผ ์ถ๊ฐํ๋ฉด ์๋์ ๊ฐ์ ์ค๋ฅ ๋ฉ์ธ์ง๊ฐ ์ถ๋ ฅ๋๋ฉฐ ํ๋ก์ธ์ค๊ฐ ์ข๋ฃ๋๋ค.

java.lang.IllegalStateException: Ambiguous mapping. Cannot map 'testController' method

์ฒซ ๋ฒ์งธ์ ์ธ ๋ฒ์งธ ๋ฉ์๋์ ๋งคํ ๊ฒฝ๋ก๊ฐ ๊ฒน์น๊ธฐ ๋๋ฌธ์ด๋ค.

์ฌ์ค ๋ ๋ฒ์งธ ๋ฉ์๋๋ `required = false`์ด๊ธฐ ๋๋ฌธ์ ๋งค๊ฐ๋ณ์๋ฅผ ์ ๋ฌํ์ง ์์ผ๋ฉด ๊ฒฝ๋ก๊ฐ ๊ฒน์น๊ฒ ๋๋ค. ํ์ง๋ง ์ด ๊ฒฝ์ฐ์๋ ์ฒซ ๋ฒ์งธ ๋ฉ์๋๊ฐ ์คํ๋์๋ค.

### @RequestBody
์ ๋ฌํ๊ณ ์ ํ๋ ๋ฆฌ์์ค๊ฐ **๋ณต์ก**ํ ๋ ์ฌ์ฉํ๋ค. ์๋ฅผ ๋ค์ด String, int๊ฐ์ ๊ธฐ๋ณธ ์๋ฃํ์ด ์๋๋ผ **๊ฐ์ฒด**์ฒ๋ผ ๋ณต์กํ ์๋ฃํ์ ํต์งธ๋ก ์์ฒญ์ ๋ณด๋ด๊ณ  ์ถ์ ๋ ์ฌ์ฉํ๋ค.

์ด ๋ ๋ฐ์ดํฐ๋ **DTO**๋ผ๋ ๊ฐ์ฒด์ ์ ์ฅ๋์ด ์ ๋ฌ๋๋ค. 

```Java
@Data
public class TestRequestBodyDTO {
	private int id;
	private String message;
}
```	

> `@Data`๋ `@Getter`, `@Setter`, `@RequiredArgsConstructor`, `@ToString`, `@EqualsAndHashCode`๋ฅผ ํ ๋ฒ์ ์ค์ ํด์ฃผ๋ lombok ์ ๋ธํ์ด์์ด๋ค.

```Java
@PostMapping("/testRequestBody")
public String testRequestBody(@RequestBody TestRequestBodyDTO testRequestBodyDTO) {
	return "id : " + testRequestBody.getId() + "\nmessage : " + testRequestBody.getMessage()";
}
```

`@RequestBody TestRequestBodyDTO testRequestBodyDTO` : RequestBody๋ก ์ ๋ฌ๋๋ JSON์ TestRequestBodyDTO ๊ฐ์ฒด๋ก ๋ณํํด ๊ฐ์ ธ์จ๋ค.

## @ResponseBody

์์ฒญ์ ๋ํ ์๋ต์ผ๋ก ๊ฐ์ฒด๋ฅผ ๋ฐํํ  ์ ์๋ค. `@RestController`๋ `@Component`์ `@ResponseBody`์ ์กฐํฉ์ผ๋ก ์ด๋ฃจ์ด์ ธ ์๋ค.

`@ResponseBody` ์ ๋ธํ์ด์์ด ๋ถ์ ๋ฉ์๋๊ฐ ๋ฐํํ ๊ฐ์ฒด๋ ์คํ๋ง์ ์ํด JSON ํํ๋ก ๋ณํ๋๊ณ  HttpResponse ๊ฐ์ฒด์ ๋ด๊ฒจ ๋ฐํ๋๋ค.
