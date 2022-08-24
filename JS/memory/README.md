# JavaScript의 메모리 구조

JavaScript 엔진은 **Heap**과 **Stack**을 관리한다. 이 두 종류의 메모리에 runtime data가 저장된다.

> ### references 🔗      
> https://valerii-udodov.com/posts/javascript-memory/#:~:text=In%20JavaScript%20(similarly%20to%20many,Stack%20is%20smaller%20and%20faster.     
> https://developer.mozilla.org/en-US/docs/Glossary/Hoisting     
> https://codeburst.io/explaining-value-vs-reference-in-javascript-647a975e12a0  

## Contents		
* ### [Stack](https://github.com/mingeun2154/skill/tree/main/JS/memory#stack-1)      
* ### [Heap](https://github.com/mingeun2154/skill/tree/main/JS/memory#heap-1)      
* ### [Hoisting](https://github.com/mingeun2154/skill/tree/main/JS/memory#hoisting-1)      
* ### [Reference](https://github.com/mingeun2154/skill/tree/main/JS/memory#reference-1)

#    

## Stack
모든 **primitive type data**(`number`, `boolean`, `string`, `Bigint`, `null`, `undefined`)들은 스택 영역에 저장된다.


## Heap
primitive type data를 제외한 나머지가 저장된다.

## Hoisting
인터프리터가 변수와 함수에 필요한 메모리 공간을 선언 전에 미리 할당하는 것.

### function hoising
```JavaScript
catName("Tiger");

function catName(name) {
  console.log(`My cat's name is ${name}`);
}
```

> 정상적으로 실행된다. "My cat's name is Tiger" 출력

### variable hoisting
* `var` - 변수의 선언을 scope의 맨 위로 올려주지만, **초기화는 예정대로 진행된다.**
* 생략 - 초기화 전에 접근 불가능
	```JavaScript
	console.log(num); // Throws ReferenceError exception - the interpreter doesn't know about `num`.
	num = 6; // Initialization
	```

* `let` - 초기화 하기 전에 접근 할 수 없다. ReferenceError 발생.
	```JavaScript
	console.log(num); // Throws ReferenceError exception as the variable value is uninitialized
	let num = 6; // Initialization
	```
	block이 시작되고 `let`, `const` 변수가 초기화되기 전까지의 영역을 **TDZ(Temporal Dead Zone)**라고 한다.

### class hoisting

```JavaScript
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
``` 
> class declaration

class declaration을 통해 생성된 클래들은 hoist되지만 초기화될때까지 접근할 수 없다. ReferenceError 발생.

### function expression and class expression
function **expression**과 class **expression**은 hoisting되지 않는다.

## reference
* passed by value - `boolean`, `null`, `undefined`, `string`, `number`
* passed by value - `Array`, `Function`, `Object` 이 세 가지는 엄밀히 말하면 모두 `Object`이다.

**non-primitive type의 값이 대입된 변수**들은 실제로 그 값을 저장하는 것이 아니라 그 **값에 대한 reference를 저장한다.**

reference는 객체가 저장된 메모리의 장소를 가리킨다.


