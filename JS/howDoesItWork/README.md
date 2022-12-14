# How browsers execute JavaScript?

JavaScript์ ์คํ
> ### references ๐   
> https://www.javascripttutorial.net/javascript-execution-context/    
> https://www.javascripttutorial.net/javascript-call-stack/     
> https://www.javascripttutorial.net/javascript-event-loop/    

## Contents		
* ### [Runtime](https://github.com/mingeun2154/skill/tree/main/JS/howDoesItWork#runtime-1)      
* ### [Execution Context](https://github.com/mingeun2154/skill/tree/main/JS/howDoesItWork#execution-context-1)      
* ### [Call Stack](https://github.com/mingeun2154/skill/tree/main/JS/howDoesItWork#call-stack-1)      
* ### [Event Loop](https://github.com/mingeun2154/skill/tree/main/JS/howDoesItWork#event-loop-1)      

#    

## Runtime
> ์คํ์ค์ธ ์์ , ๋๋ ์คํํ๊ฒฝ์ ์๋ฏธํ๋ค.

JavaScript์ ๋ฐํ์ ๊ตฌ์กฐ

<img src="./img/JS-runtime.jpeg" width="80%" alt="๋ฐํ์ ๊ตฌ์กฐ">

> ํฐ ๊ทธ๋ฆผ์ ๋จผ์  ํ์ํ๊ณ  ๊ฐ ๋ถ๋ถ๋ค์ ๋ํด ์์๋ณด์.

## Execution Context
> ์๋๋ฐฉ์ ๋ง์ ์ดํดํ๋ ค๋ฉด ๋งฅ๋ฝ์ ์๊ณ  ์์ด์ผ ํ๋ค. ๋๊ฐ์ ๋จ์ด๋ผ๋ ๋งฅ๋ฝ์ ๋ฐ๋ผ ์๋ฏธ๊ฐ ๋ฌ๋ผ์ง๊ธฐ ๋๋ฌธ์ด๋ค.    
> ์ฝ๋๋ ๋ง์ฐฌ๊ฐ์ง์ด๋ค.   
> execution context๋ ๋ง ๊ทธ๋๋ก **์ฝ๋ ์คํ์ ๊ดํ ๋งฅ๋ฝ**์ ์ถ์ํํ ๊ฐ๋์ด๋ค.    

JavaScript engine์ด ์๋ฐ์คํฌ๋ฆฝํธ ์ฝ๋๋ฅผ ์คํ์ํฌ ๋, ์์ง์ execution context๋ฅผ ์์ฑํ๋ค.    

execution context๋ **๋ ๊ฐ์ง ๋จ๊ณ(creation phase(์ด๊ธฐํ)์ execution phase(์คํ))**๋ฅผ ๊ฑฐ์น๋ค


์๋์ ์ฝ๋๊ฐ ์คํ๋๋ ๊ณผ์ ์ ์ดํด๋ณด์.    

```JavaScript
let x = 10;

function timesTen(a){
    return a * 10;
}

let y = timesTen(x);

console.log(y); // 100

```
### creation phase
> ์๋ฐ์คํฌ๋ฆฝํธ ์์ง์ด **์คํฌ๋ฆฝํธ๋ฅผ ์ฒ์ ์คํ** ํ ๋ global execution context๋ฅผ ์์ฑํ๋ค.  

global scpoe์ ์ ์ธ๋ ํจ์์ ๋ณ์๋ค์ context์ ๋ฑ๋กํ๋ค(์์ง ๊ฐ์ด ์ด๊ธฐํ๋์ง๋ ์๋๋ค).

๐๐๐๐ ๐. global execution context ์์ฑ(runtime์ ๋ํ ํ๊ฒฝ์ค์ ์ด๋ผ๊ณ  ๋ณผ ์ ์๋ค.)    

* global object ์์ฑ(web browser:`window`, Node.js:`global`)    
* `this` ๊ฐ์ฒด๋ฅผ ์์ฑํ๊ณ  `global object`์ bindingํ๋ค.     
* ๋ณ์๋ค๊ณผ function references๋ฅผ ์ํ heap memory ์ค์ .     
* ์ ์ธ๋ ํจ์๋ค์ heap์ ์ ์ฅํ๊ณ  ๋ณ์๋ค์ global execution context์ ํฌํจ๋ ๋ณ์๋ค์ `undefined`๋ก ์ด๊ธฐํํ๋ค.    

๐๐๐๐ ๐. ๋ณธ๊ฒฉ์ ์ผ๋ก ์์ ์ฝ๋๋ฅผ ์คํํ๊ธฐ ์ํ ์ค์    
* `x`์ `y`์ ํจ์ `timesTen()`์ global execution context์ ์ ์ฅํ๋ค.
* `x`, `y`๋ฅผ `undefined`๋ก ์ด๊ธฐํํ๋ค.
	
<img src="./img/creation-phase-1.jpeg" width="30%" alt="creation-phase">    

> creation phase๊ฐ ๋๋๋ฉด global execution context๋ ์ด๋ฐ ๋ชจ์ต์ด๋ค.

### execution phase
> creation phase๊ฐ ๋๋๋ฉด global execution context๋ execution phase๋ก ๋์ด๊ฐ๋ค.     

execution phase๋์ ์๋ฐ์คํฌ๋ฆฝํธ ์์ง์ **์ฝ๋๋ฅผ ํ ์ค ์ฉ ์คํํ๋ค.** **๋ณ์์ ๊ฐ์ ๋์**ํ๊ณ  **ํจ์์ ํธ์ถ**์ ์คํํ๋ค.

์ฝ๋๋ฅผ ์คํํ๋ค๊ฐ ํจ์ ํธ์ถ์ ๋ง๋๋ฉด ์์ง์ **function execution context๋ฅผ ์ด๊ธฐํ**ํ๋ค.

function execution context์ global execution context๋ ์ ์ฌํ๋ค.

function execution context์์๋ global object๋ก `arguments`๊ฐ ์์ฑ๋๋ค. ์ด ๊ฐ์ฒด๋ฅผ ํตํด ์ ๋ฌ๋ฐ์ ๋ชจ๋  argument์ ์ ๊ทผํ  ์ ์๋ค.

`this`๋ caller์ธ window๋ฅผ ๊ฐ๋ฆฌํค๊ณ  ์๋ค.

<img src="./img/execution-phase-1.jpeg" width="60%" alt="execution-phase-1">

> ๋ณ์์ ๊ฐ์ด ๋์๋๊ณ  ํจ์ ํธ์ถ์ ์ํ context๊ฐ ์์ฑ๋์๋ค.

function execution context ์ด๊ธฐํ๊ฐ ๋๋๋ฉด ์์ง์ **์ด context์ ๋ํ execution phase๋ก ์ง์**ํ๋ค.
<img src="./img/execution-phase-2.jpeg" width="60%" alt="execution-phase-2">
> a์ 10์ด ๋์๋๊ณ  ํจ์์ ๊ฒฐ๊ณผ๊ฐ global execution context๋ก return๋๋ค. 

## Call Stack
> execution context(global, function execution context)๋ค์ ๊ด๋ฆฌํ๋ ์๋ฃ๊ตฌ์กฐ์ด๋ค.

### ๋ธ๋ผ์ฐ์ ๊ฐ call stack์ ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ
* JavaScript ํ์ผ์ ์คํํ๋ฉด ์์ง์ global execution context๋ฅผ ์์ฑํด์ call stack์ top์ pushํ๋ค.
* ํจ์๊ฐ ํธ์ถ๋ ๋๋ง๋ค, ์์ง์ **function execution context๋ฅผ ์์ฑํ๊ณ  call stack์ pushํ๊ณ , ํจ์๋ฅผ ์คํ**ํ๋ค.
* ํจ์๊ฐ ๋ค๋ฅธ ํจ์๋ฅผ ํธ์ถํ  ๊ฒฝ์ฐ, ์์ง์ function execution context๋ฅผ ์์ฑํ๊ณ  call stack์ pushํ๊ณ , ํจ์๋ฅผ ์คํํ๋ค.    
์๋ก push๋ ํจ์๊ฐ ์ข๋ฃ๋๋ฉด ๊ทธ context๋ ์คํ์์ ์ ๊ฑฐ๋๊ณ  ์ด์ ์ ์คํํ๋ ํจ์๋ฅผ ์ด์ด์ ์คํํ๋ค.
* script๋ call stack์ด ๋น ๋๊น์ง ์คํ๋๋ค.

### call stack example

```JavaScript
function add(a, b) {
    return a + b;
}

function average(a, b) {
    return add(a, b) / 2;
}

let x = average(10, 20);
```

* global execution context(`main()` ๋๋ `global()`๋ก ํํ๋๋ค.)
	* creation phase - window, this, ์ ์ญ๋ณ์์ ํจ์ ๋ฑ๋ก
	* execution phase - ์ฝ๋๋ฅผ ํ ์ค ์ฉ ์คํ
* `average()` ํจ์์ ๋ํ context๋ฅผ ์์ฑํ์ฌ call stack์ ์ถ๊ฐ.
	* ์์ง์ call stack์ top์ ์๋ `average()` ํจ์๋ฅผ ์คํํ๋ค.
* `add()` ํจ์์ ๋ํ context๋ฅผ ์์ฑํ์ฌ call stack์ ์ถ๊ฐํ๋ค.
	* `add()` ํจ์๊ฐ ์คํ, ์ข๋ฃ๋๊ณ  ์คํ์์ ์ ๊ฑฐ๋๋ค.
* ์คํ์ top์ ์๋ `average()`๊ฐ ๋ค์ ์คํ๋๋ค.

<img src="./img/call-stack-flow.jpeg" alt="์ฝ ์คํ์ ์ํ">

> ์์ ์ฝ๋๊ฐ ์คํ๋๋ ๋์์ call stack์ ๋ณํ.   
> call stack์ top์ ์๋ ํจ์๊ฐ ํ์ฌ ์คํ์ค์ธ ํจ์์ด๋ค.

<img src="./img/inside-call-stack.jpeg" alt="context๋ค์ ์ํ">

> ์์ ์ฝ๋๊ฐ ์คํ๋๋ ๊ณผ์ ์ ์ข ๋ ์์ธํ ๋ํ๋ธ ๊ทธ๋ฆผ.   

๋ชจ๋  execution context๋ค์ **์ด๊ธฐํ(symbol ๋ฑ๋ก, undefined๋ก ์ด๊ธฐํ)**, **์คํ(symbol์ ๊ฐ์ ๋์ํ๊ณ  ๊ณ์ฐ)์ ๋จ๊ณ**๋ฅผ ๊ฑฐ์น๋ค.

### Stack Overflow
**call stack์ ํฌ๊ธฐ๋ ๊ณ ์ **๋์๋ค. (ํฌ๊ธฐ๋ host environment์ ๋ฐ๋ผ ๋ค๋ฅด๋ค.)

execution context๊ฐ call stack์ ํฌ๊ธฐ๋ณด๋ค ๋ง์์ง๋ฉด stack overflow error๊ฐ ๋ฐ์ํ๋ค.

```JavaScript
function fn() {
    fn();
}

fn(); // stack overflow
```

## Event Loop

JavaScript๋ **single-threaded** programming language์ด๋ค. (JavaScript๋ก๋ **ํ ๋ฒ์ ํ๋์ ์์(ํจ์)๋ง ์คํ**ํ  ์ ์๋ค.)

์๋ฐ์คํฌ๋ฆฝํธ ์์ง์ ๋ค์๊ณผ ๊ฐ์ ๊ณผ์ ์ ๋ฐ๋ณตํ๋ฉฐ ์ฝ๋๋ฅผ ์์์๋ถํฐ ์๋๋ก ํ ์ค ์ฉ ์คํํ๋ค.
* **creation phase** - execution context๋ฅผ ๋ง๋ค์ด์ call stack์ push.
* **execution phase** - call stack์ top์ ์๋ ํจ์๋ฅผ ์คํํ๊ณ  ์คํ์์ ์ ๊ฑฐํ๋ค.

### blocking function
**์คํ์๊ฐ์ด ๊ธด** ํจ์. ํด๋น ์๊ฐ๋์ ์น ํ์ด์ง์ ๋ชจ๋  interaction์ด ์ฐจ๋จ๋๋ค. (์ฌ์ฉ์๊ฐ ์ด๋ ํด๋ฆญํด๋ ๋ฐ์ํ์ง ์๋๋ค.)

### example : blocking function

```JavaScript
function task(message) { // blocking function
    // emulate time consuming task
    let n = 10000000000;
    while (n > 0){
        n--;
    }
    console.log(message);
}

console.log('Start script...');
task('Call an API');
console.log('Done!');

// ์คํ๊ฒฐ๊ณผ
Start script.... // 13์ด ๋ค ๋ค์ ๋ฌธ์ฅ์ด ์ถ๋ ฅ๋์๋ค. 13์ด ๋์ ์น์ฌ์ดํธ(์ ํ๋ธ) ์ด๋๋ฅผ ํด๋ฆญํด๋ ๋ฐ์์ด ์์๋ค.
Call an API.
Done!
```

### example : callback
> callback์ด๋ **๋์ค์ ์คํํ๊ธฐ ์ํด** ๋ค๋ฅธ ํจ์์๊ฒ ์ธ์๋ก์ ๋๊ฒจ์ฃผ๋ ํจ์์ด๋ค. 

```JavaScript
console.log('Start script...');

setTimeout(() => {
    task('Download a file.');
}, 1000);

console.log('Done!');

// ์คํ๊ฒฐ๊ณผ
Start script.... 
Done! // 13์ด ๋ค ๋ค์ ๋ฌธ์ฅ์ด ์ถ๋ ฅ๋์๋ค. 13์ด ๋์ ๋ฐ์์ด ์๋ ๊ฒ์ ๋์ผํ๋ค.
Call an API.
```
์์ ์ฝ๋์์๋ `Start script...` ์ `Done!` ์ด ๋ฐ๋ก ์ถ๋ ฅ๋๋ค.

์์ ๋งํ๋ฏ, JavaScript ์์ง์ ํ ๋ฒ์ ํ๋์ ์์๋ง ํ  ์ ์๋ค. 

์กฐ๊ธ ๋ ์ ํํ ๋งํ์๋ฉด, **JavaScript runtime**์ ํ ๋ฒ์ ํ ๊ฐ์ง ์ผ๋ง ํ  ์ ์๋ค.

์น ๋ธ๋ผ์ฐ์ ๋ JavaScript ๋ฟ๋ง ์๋๋ผ ๋ค๋ฅธ component๋ฅผ ๊ฐ์ง๊ณ  ์๋ค.

ํ๋ก๊ทธ๋๋จธ๊ฐ `setTimeout()`, `fetch()`, `eventListner()` ๋ฑ์ ํธ์ถํ๋ฉด **๋ธ๋ผ์ฐ์ ๋ ์ด ์์๋ค์ ๋์์, ๋น๋๊ธฐ์ ์ผ๋ก ์ฒ๋ฆฌํ๋ค.** 

`setTimeout()`, fetch request, DOM event๋ ๋ชจ๋ ์น ๋ธ๋ผ์ฐ์ ์ **Web APIs**์ ์ผ๋ถ๋ถ์ด๋ค.

### example : setTimeout()์ ์คํ
* ์ฝ๋๋ฅผ ์คํํ๋ค๊ฐ `setTimeout()` ํจ์๋ฅผ ๋ง๋๋ค.
* `setTimeout()` ์ ๋ํ context๋ฅผ ๋ง๋ค์ด stack์ ๋ฃ๊ณ  ์คํํ๋ค.
	* Web API๊ฐ 1์ด๋ฅผ ์ธก์ ํ๋ timer๋ฅผ ์์ฑํ๋ค. `setTimeout()`์ด stack์์ ์ ๊ฑฐ๋๋ค.
* `console.log('Done!')` ์ด ์คํ๋๋ค. **๋์์ timer๋ ์๊ฐ์ ์ฌ๊ณ  ์๋ค.**
* timer๊ฐ ๋ง๋ฃ๋๋ฉด Web API์ ์ํด `task()`๊ฐ callback queue์ ์ฝ์๋๋ค.
* event loop๋ ์ง์์ ์ผ๋ก callback queue์ call stack์ ๊ฐ์ํ๋ค.
* **call stack์ ๋ ์ด์ ์คํํจ ํจ์๊ฐ ์๋ ๊ฒฝ์ฐ**, event loop๋ callback queue์ ํจ์๋ฅผ call stack์ ๋ฃ๋๋ค.

<img src="./img/setTimeout.jpeg" width="80%" alt="setTimeout ์คํ">

`setTimeout()`์ ์ ๋ฌ๋ ์ธ์๊ฐ `0`์ธ ๊ฒฝ์ฐ์๋ ์์ ๊ฐ์ ์์๋ก ์คํ๋๋ค.
> 0์ด์ ๊ฐ์ ํน์ํ ์ผ์ด์ค์ ๋ํ ๋ณ๋์ handler๋ ์๋ค.      
> [ํน์ํ ์ผ์ด์ค๋ฅผ ๋น ๋ฅด๊ฒ ์ฒ๋ฆฌํ๋ ค๊ณ  ํ  ์๋ก ์ฝ๋๊ฐ ๋ณต์กํด์ง๊ณ  ์ฑ๋ฅ๋ฉด์์๋ ๋นํจ์จ์ ์ด๋ค.](https://github.com/mingeun2154/CS/tree/main/ComputerArchitecture/eightGreatIdea#3-make-the-common-case-fast)
