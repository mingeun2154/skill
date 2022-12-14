# Promise

> ### references ๐  
> React.js, ์คํ๋ง ๋ถํธ, AWS๋ก ๋ฐฐ์ฐ๋ ์น ๊ฐ๋ฐ 101		- ๊น๋ค์  -    
> https://www.w3schools.com/js/js_promise.asp     
> https://ko.javascript.info/promise-basics

## Contents		
* ### [Promise ์์ฑ](https://github.com/mingeun2154/skill/tree/main/JS/promise#promise-1)      
* ### [Promise์ ์ํ](https://github.com/mingeun2154/skill/tree/main/JS/promise#promise%EC%9D%98-%EC%83%81%ED%83%9C-1)
* ### [then()](https://github.com/mingeun2154/skill/tree/main/JS/promise#then-1)      
* ### [catch()](https://github.com/mingeun2154/skill/tree/main/js/promise#catch-1)
* ### [finally()](https://github.com/mingeun2154/skill/tree/main/js/promise#finally-1)
* ### [Promise Chaining](https://github.com/mingeun2154/skill/tree/main/JS/promise#promise-chaining-1)

## Promise
**์ํ๋ ์์(executor)๊ณผ ๊ทธ ๊ฒฐ๊ณผ๊ฐ**์ ๊ฐ์ธ๋ ๊ฐ์ฒด์ด๋ค. executor๋ฅผ ์คํ์ํค๊ณ  ๊ทธ ๊ฒฐ๊ณผ๋ฅผ ํํํ๋ค.

์ฃผ๋ก **๋น๋๊ธฐ ์์**์ ์คํ์ํจ๋ค.

`Promise`๊ฐ์ฒด๋ ์๋์ ๊ฐ์ ๋ฐฉ์์ผ๋ก ๋ง๋ค ์ ์๋ค.

์์ฑ์์ ์ ๋ฌ๋๋ ํจ์๋ **executor**๋ผ๊ณ  ํ๋ฉฐ **๊ฒฐ๊ณผ๋ฅผ ๋ง๋ค์ด๋ด๋ ์ฝ๋**๋ฅผ ํฌํจํ๋ค.

executor๋ **๊ฐ์ฒด๊ฐ ์์ฑ๋  ๋ ์๋์ผ๋ก ์คํ**๋๋ค.

`resolve`์ `reject`๋ JavaScript๊ฐ ์ ๊ณตํ๋ ์ฝ๋ฐฑ์ด๋ค. ๊ฐ๋ฐ์๋ ์ ๊ฒฝ์ฐ์ง ์๊ณ  executor ๋ด๋ถ์ ์ฝ๋๋ง ์์ฑํ๋ฉด ๋๋ค.

```JavaScript
let promise = new Promise(function(resolve, reject){
		// executor
		// case1. ์ฑ๊ณต - resolve(value) ํธ์ถ
		// case2. ์คํจ - reject(error) ํธ์ถ
		});
```

executor ๋ด๋ถ์์๋ ๋ฐ๋์ `resolve()`์ `reject()`ํจ์ ๋ ์ค ํ๋๋ฅผ ํธ์ถํด์ผ ํ๋ค.
* `resolve(value)` - ์์์ด ์ฑ๊ณต์ ์ผ๋ก ๋๋ ๊ฒฝ์ฐ **๊ทธ ๊ฒฐ๊ณผ๋ฅผ ํํ**ํ๋ `value`์ ํจ๊ป ํธ์ถํ๋ค.
* `reject(error)` - ์๋ฌ๊ฐ ๋ฐ์ํ ๊ฒฝ์ฐ **์๋ฌ๋ฅผ ํํ**ํ๋ `error`์ ํจ๊ป ํธ์ถํ๋ค.

<img src="./img/promise-example-1.png" width="50%" alt="promise-example-1">

* executor : `promise` ์์ฑ๊ณผ ๋์์ `setTimeout()`์ด ์ ๋ฌ๋ฐ์ ํจ์๊ฐ ์คํ๋๋ค. `flag`๊ฐ 3์ ๋ฐฐ์์ด๋ฉด ์ฑ๊ณต, ์๋๋ฉด ์คํจ์ด๋ค. 
* `result` : `promise`๊ฐ ์คํํ๋ executor์ ์คํ๊ฒฐ๊ณผ๋ฅผ ํํํ๋ค.
* `reject()`, `resolve()`๋ฅผ ํธ์ถํจ์ผ๋ก์จ main thread์ ์คํ ๊ฒฐ๊ณผ๋ฅผ ์๋ ค์ค๋ค(`result`๊ฐ์ฒด๊ฐ ์ ๋ฌ๋๋ค.)

## Promise์ ์ํ
`Promise` ๊ฐ์ฒด๋ **์ธ ๊ฐ์ง ์ํ**๋ฅผ ๊ฐ์ง๋ค.
* pending : fulfilled๋ ์๋๊ณ  reject ์ํ๋ ์๋ ์ด๊ธฐ์ํ
* fulfilled : executor์ ์คํ ์ฑ๊ณต์ ์ผ๋ก ์๋ฃ๋ ์ํ
* rejected : executor์ ์คํ์ด ์คํจํ ์ํ

executor์ ์คํ์ด `Promise`์ ์ํ๋ฅผ ๋ ์ค ํ๋๋ก ๋ณํ์ํจ๋ค.

<img src="./img/executor.png" width="70%" alt="executor์ ์คํ">

> `state`์ `result` ํ๋กํผํฐ๋ ๋ด๋ถ ํ๋กํผํฐ๋ก ๊ฐ๋ฐ์๊ฐ ์ง์  ์ ๊ทผํ  ์ ์๋ค.   
> `then`, `catch`, `finally`๋ฅผ ์ฌ์ฉํ๋ฉด ์ ๊ทผํ  ์ ์๋ค.

์ด๋ ๊ฒ resolved(์ดํ) ๋๋ rejected(๊ฑฐ๋ถ)๋ ์ํ์ `Promise`๊ฐ์ฒด๋ **settled Promise**(์ฒ๋ฆฌ๋ Promise)๋ผ๊ณ  ํ๋ค. 

๋ฐ๋๋ pending(๋๊ธฐ์ํ) Promise์ด๋ค.

## then()
`Promise.then()` ๋ฉ์๋๋ฅผ ์ฌ์ฉํด์ ์ฑ๊ณต, ์คํจ์ ๋ํ ์ฝ๋ฐฑ์ ์ง์ ํ  ์ ์๋ค. ๋ ๋ค ํ ์๋ ์๋๋ค.

`then()`**์ผ๋ก ์ ๋ฌํ๋ ๋ฉ์๋์ parameter์๋** `Promise`**๊ฐ resolveํ ๊ฐ์ด ์ ๋ฌ๋๋ค.**

```JavaScript
myPromise.then(
		function(value) {/* ์ฑ๊ณต ์ ์คํ๋๋ ์ฝ๋ */}, 
		function(error) {/* ์คํจ ์ ์คํ๋๋ ์ฝ๋ */}
);
```

`then()`์ ์ฒซ ๋ฒ์งธ ์ธ์๋ promise๊ฐ resolve(์ฑ๊ณต)ํ์ ๋ ์คํ๋๋ ํจ์์ด๋ค. ์คํ ๊ฒฐ๊ณผ๋ฅผ ์ธ์๋ก ๋ฐ๋๋ค.

`then()`์ ๋ ๋ฒ์งธ ์ธ์๋ promise๊ฐ rejected(์คํจ)๋์์ ๋ ์คํ๋๋ ํจ์์ด๋ค. ์ธ์๋ก ์๋ฌ๋ฅผ ๋ฐ๋๋ค.

```JavaScript
let promise = new Promise(function(resolve, reject) {
  setTimeout(() => reject(new Error("์๋ฌ ๋ฐ์!")), 1000);
});

// reject ํจ์๋ .then์ ๋ ๋ฒ์งธ ํจ์๋ฅผ ์คํํฉ๋๋ค.
promise.then(
  result => alert(result), // ์คํ๋์ง ์์
  error => alert(error) // 1์ด ํ "Error: ์๋ฌ ๋ฐ์!"์ ์ถ๋ ฅ
);
```

> `reject()`ํจ์๋ก ์ ๋ฌํ  error๋ `Error`๊ฐ์ฒด๋ฅผ ์์ํ๋ ๊ฐ์ฒด๋ฅผ ์ฌ์ฉํ๋ ๊ฒ์ด ์ข๋ค.

## catch()
`catch(f)`๋ `then(null, f)`๊ณผ ์๋ฒฝํ ๊ฐ๋ค.

## finally()
`Promise`๊ฐ ์ฒ๋ฆฌ๋๊ธฐ๋ง ํ๋ฉด ํญ์ ์คํ๋๋ค.

ํ๋ฉด์ ๋ ์ด์ ๊ทธ๋ง ํ์๋์ด๋ ๋๋ loading indicator๋ฅผ ๋ฉ์ถ๋ ๊ฒฝ์ฐ์ ๊ฐ์ด, **๊ฒฐ๊ณผ๊ฐ ์ด๋ป๋  ๋ง๋ฌด๋ฆฌ๊ฐ ํ์ํ ๊ฒฝ์ฐ**์ ์ ์ฉํ๋ค.

* `then()`์ ์ ๋ฌ๋๋ ํธ๋ค๋ฌ์ ๋ค๋ฅด๊ฒ ์ธ์๊ฐ ์๋ค.(์ฑ๊ณต, ์คํจ ์ฌ๋ถ๋ฅผ ๋ชฐ๋ผ๋ ๋๊ธฐ ๋๋ฌธ์ด๋ค.)

* `finally` ํธ๋ค๋ฌ๋ ์๋์ผ๋ก **๋ค์ ํธ๋ค๋ฌ์ ๊ฒฐ๊ณผ์ ์๋ฌ๋ฅผ ์ ๋ฌ**ํ๋ค.

```JavaScript
new Promise((resolve, reject) => {
  setTimeout(() => resolve("๊ฒฐ๊ณผ"), 2000)
})
  .finally(() => alert("ํ๋ผ๋ฏธ์ค๊ฐ ์ค๋น๋์์ต๋๋ค."))
  .then(result => alert(result)); // <-- .then์์ result๋ฅผ ๋ค๋ฃฐ ์ ์์
```

`finally`๋ `Promise`์ ๊ฒฐ๊ณผ๋ฅผ ์ฒ๋ฆฌํ๊ธฐ ์ํด ๋ง๋ค์ด์ง ๊ฒ ์๋๋ค.  ๊ฒฐ๊ณผ๋ `Promise`๋ฅผ **ํต๊ณผ**ํ๋ค.

## Promise Chaining
promise๊ฐ resolveํ ๊ฒฐ๊ณผ๊ฐ `then` ํธ๋ค๋ฌ์ chain(์ฌ์ฌ)์ ๋ฐ๋ผ ๊ณ์ ์ ๋ฌ๋๋ค. 

`then`์ `Promise`๋ฅผ ๋ฐํํ๋ค. ํธ๋ค๋ฌ๊ฐ ๋ฐํํ๋ ๊ฐ์ด `Promise`์ `result`๊ฐ ๋๋ค.

```JavaScript
new Promise(function(resolve, reject) {
    setTimeout(() => resolve(1), 1000);
}).then((result) => {
    result=result*2;
    console.log(result);
    return result;
}).then((result) => {
    result=result*2;
    console.log(result);
    return result;
}).then((result) => {
    result=result*2;
    console.log(result);
    return result;
});
```

### ํธ๋ค๋ฌ๊ฐ Promise๋ฅผ ๋ฐํํ๋ ๊ฒฝ์ฐ
`then(handler)`์ handler๊ฐ `Promise`๋ฅผ ์์ฑํ๊ฑฐ๋ ๋ฐํํ๋ ๊ฒฝ์ฐ๋ ์๋ค.

์ด ๊ฒฝ์ฐ `Promise`๋ฅผ ๋ฐํํ๋ ํธ๋ค๋ฌ ์ดํ์ ํธ๋ค๋ฌ๋ค์ ์ด `Promise`๊ฐ ์ฒ๋ฆฌ๋  ๋๊น์ง ๊ธฐ๋ค๋ ธ๋ค๊ฐ ๊ทธ ๊ฒฐ๊ณผ๋ฅผ ๋ฐ๋๋ค.

```JavaScript
new Promise(function(resolve, reject) {

  setTimeout(() => resolve(1), 1000);

}).then(function(result) {

  alert(result); // 1

  return new Promise((resolve, reject) => { // (*)
    setTimeout(() => resolve(result * 2), 1000);
  });

}).then(function(result) { // (**)

  alert(result); // 2

  return new Promise((resolve, reject) => {
    setTimeout(() => resolve(result * 2), 1000);
  });

}).then(function(result) {

  alert(result); // 4

});
```
