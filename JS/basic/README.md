# JavaScript Basic

자바스크립트의 기본
> ### references 🔗  
> https://www.javascripttutorial.net/javascript-data-types/   
> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var    
> https://stackoverflow.com/questions/762011/what-is-the-difference-between-let-and-var

## Contents		
* ### [Data Type](https://github.com/mingeun2154/skill/tree/main/JS/basic#data-type-1)      
* ### [변수 선언](https://github.com/mingeun2154/skill/tree/main/JS/basic#declare-variable)      

#    

## Data Type
자바스크립트의 자료형은 크게 두 가지로 나뉜다. **primitive**와 **complex**이다.  

* primitive type : `null`, `undefined`, `boolean`, `number`, `string`, `symbol`, `bigint`
* complex type : `object`

JavaScript는 **dynamically typed languaged**이다. 

변수가 특정 타입에 연관되지 않기 때문에 **여러 가지 타입**의 값을 가질 수 있다.

변수의 타입은 `typeof()` 연산자로 알 수 있다.

```JavaScript
let counter = 120;
console.log(typeof(counter)); // "number"

counter = false;
console.log(typeof(counter)); // "boolean"

counter = "Hi";
console.log(typeof(counter)); // "string"
```

### undefined
그 자체로 값인 타입이다. `undefined`타입 변수는 값으로 `undefined`만 가질 수 있다.

변수가 선언되고 초기화되지 않을 경우, 자동으로 `undefined` 값이 대입된다.

### null
undefined와 비슷하다. `null` 타입 변수는 그 값으로 `null`만을 가질 수 있다.

```JavaScript
let obj = null;
console.log(typeof obj); // object

console.log(null == undefined); // true
```
> JavaScript는 `null`과 `undefined`를 같은 값으로 인식한다.

`typeof null`은 결과로 `object`를 반환하는데 이것은 JavaScript의 버그이다. 

수정하면 수많은 웹사이트가 오작동하기 때문에 수정하지 않았다고 한다.

### number
정수 타입과 실수 타입을 모두 표현한다.

JavaScript는 `10.0`처럼 정수로 나타낼 수 있는 수는 정수(`10`)로 취급한다.

실수값 저장에 필요한 메모리의 크기가 정수의 두 배이기 때문이다.

* `NaN` - 유효하지 않은 수라는 의미이며 두 가지 성질을 가진다.

	```JavaScript
	console.log(NaN/2); // NaN  	  1. NaN에 대한 연산은 NaN을 반환한다.
	console.log(NaN == NaN); // false 2. NaN은 어떤 값(자신 포함)과도 같지 않다.
	```

### string 
`'` 또는 `"`으로 시작해서 끝난다.

JavaScript string은 **immutable**이기 때문에 **문자 단위로 값을 바꿀 수 없다**. 

새로운 문자열을 생성해서 **문자열 통째로 덮어쓸 수는 있다.**

> C의 상수 포인터와 같은 원리이다. 내부적으로 상수 포인터를 유지하는 것 같다.

### boolean
`true` 또는 `false` 를 값으로 가진다.

`Boolean()`함수를 사용하면 다른 타입의 값을 `boolean` 타입으로 바꿀 수 있다.

|Type     |ture                        |false       |
|---------|----------------------------|------------|
|string 	|non-empty string            |empty string|
|number	  |non-zero number and infinity|0, NaN      |
|object	  |non-null object             |null        |
|undefined|	                           |undefined   |

굳이 Boolean() 함수를 안 써도 위의 값들로 인식한다.    

**단,** `if(x==true)` **와 같이** `boolean` **과 직접 비교하면 안된다.**

```JavaScript
function checkBoolValue(x){
    if(x)
        console.log("true");
    else
        console.log("false");
}

const _number_true = 10;
let _number_false;

const _object_true = {name: "some object"};
let _object_false = null;

checkBoolValue(_number_true);
checkBoolValue(_number_false);
checkBoolValue(_object_true);
checkBoolValue(_object_false);
```

### symbol
ES6부터 추가된 primitive type이다. 다른 타입들과 다르게 **literal form을 가지지 않는다.**

symbol을 생성하려면 `Symbol()`**함수를 사용해야 한다.**

```JavaScript
let s1 = Symbol();

console.log(Symbol() == Symbol()); // false
```

`Symbol()` 함수는 **호출할 때마다 unique value를 return한다.**

### bigint
2⁵³-1 보다 큰 모든 수를 표현한다. `bigint` literal을 생성하려면 숫자 뒤에 `n`을 붙이면 된다.

```JavaScript
let _bigint = 9007188254740911n;
console.log(typeof(_bigint)); // bigint
```

## Declare Variable
* `let` - immediate(가장 가까운) block scoped 변수 선언. 초기화는 선택. 

	```JavaScript
	function run() {
  var foo = "Foo";
  let bar = "Bar";

  console.log(foo, bar); // Foo Bar

  {
    var moo = "Mooo" // 이 함수 전체에서 유효하다.
    let baz = "Bazz"; // 이 블럭 내부에서만 유효하다.
    console.log(moo, baz); // Mooo Bazz
  }

  console.log(moo); // Mooo
  console.log(baz); // ReferenceError
	}

	run();
 ```

 ```JavaScript
 function checkHoisting() {
		console.log(foo); // ReferenceError
		let foo = "Foo";
		console.log(foo); // Foo
	}
	checkHoisting();
	```
	> 초기화 하기 전에 접근 할 수 없다.


* `var` - immediate function scoped 변수 선언. 초기화는 선택. 

	```JavaScript
	var x = 1;

	if (x === 1) {
		var x = 2; // 변수 x를 재할당(덮어써진다.)
		console.log(x);
		// expected output: 2
	}

	console.log(x);
	// expected output: 2
	```
	> **재할당**이 가능하다.

	```JavaScript
	var funcs = [];
	// let's create 3 functions
	for (var i = 0; i < 3; i++) {
		// and store them in funcs
		funcs[i] = function() {
			// each should log its value.
			console.log("My value: " + i);
		};
	}
	for (var j = 0; j < 3; j++) {
		// and now let's run each one to see
		funcs[j]();
	}
	```
	"My value: 3"이 세 번 출력된다. ❓이유는 잘 모르겠다.
	> `var` 키워드는 안 쓰는게 좋겠다...

	```JavaScript
	var foo = "Foo";  // globally scoped
	let bar = "Bar"; // not allowed to be globally scoped

	console.log(window.foo); // Foo
	console.log(window.bar); // undefined
	```
	> `let` 키워드로 선언한 변수는 global object의 property가 될 수 없다. (전역변수가 될 수 없다.)


* `const` - `let`과 비슷하다. block scoped 변수를 생성하지만 초기화가 필수이고 값을 변경할 수 없다.
*  생략 - 전역변수 생성
	```JavaScript
	num = 10;
	console.log(num); // 10 출력
	```
