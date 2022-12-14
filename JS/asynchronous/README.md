# Asynchronous & Synchronous

> ### references π

μΉ λΈλΌμ°μ λ **μλ°μ€ν¬λ¦½νΈ μ½λλ₯Ό νλμ threadμμ μ€ν**μν¨λ€. 

κΈ°λ³Έμ μΌλ‘ single-threaded νκ²½μμ μ€νλλ μ½λλ λκΈ°μ (synchronous)μΌλ‘ μ€νλλ€.

**νμ§λ§ μλ°μ€ν¬λ¦½νΈλ λΉλκΈ°μ (asynchronous)μΌλ‘ μ€νλλ€.**


## Contents		
* ### [Synchronous](https://github.com/mingeun2154/skill/tree/main/JS/asynchronous#asynchronous--synchronous#synchronous-1)
* ### [Asynchronous](https://github.com/mingeun2154/skill/tree/main/JS/asynchronous#asynchronous--synchronous#asynchronous-1) 
* ### [λΉλκΈ° ν¨μμ μ€ν](https://github.com/mingeun2154/skill/tree/main/JS/asynchronous#asynchronous--synchronous#asynchronous-function)

#    

## Synchronous
> λκΈ°νμ κ΄λ ¨λ κ°λλ€μ ν΅μ¬μ **μμ**μ΄λ€.

**λκΈ°μ ** = **λκΈ°νλμ΄μλ€**

**λκΈ°νλμ΄μλ€** = μ½λμ μ€νμ΄ νλ‘κ·Έλλ¨Έμ **μλν μμλ**λ‘ μ€νλλ€

κ²°κ΅­ **μ½λκ° λκΈ°μ μΌλ‘ μ€ν**λλ€λ λ»μ νλ‘κ·Έλλ¨Έκ° μμ±νλλ‘ **μμμλΆν° μλλ‘ ν μ€ μ© μ€ν**λλ€λ λ»μ΄λ€.


## Asynchronous
**λΉλκΈ°μ μΌλ‘ μ€ν**λλ€ = **λκΈ°μ μΌλ‘ μ€νλμ§ μλλ€** = μ½λκ° λμ λ³΄μ΄λ **μμλλ‘ μ€νλμ§ μλλ€**

single-threaded νκ²½μμ μ€νλλ μλ°μ€ν¬λ¦½νΈλ₯Ό λΉλκΈ°μ μΌλ‘ μ€νμν€λ μ΄μ λ λ¬΄μμΌκΉ π€

[blocking function](https://github.com/mingeun2154/skill/tree/main/JS/howDoesItWork#blocking-function)μ΄ νΈμΆλμ΄λ μΉ νμ΄μ§κ° μ μμ μΌλ‘ λμνλλ‘ νκΈ° μν¨μ΄λ€.

## Asynchronous function

### λΉλκΈ° ν¨μμ μ€ν κ³Όμ 
* JavaScript μ½λκ° μ€νλλ€κ° `setTimeout()`, `fetch()`, `eventListener()`μ κ°μ ν¨μλ€μ λ§λλ©΄ ν΄λΉ ν¨μλ€μ **Web APIμ μλ‘μ΄ thread**μμ μ€νμν¨λ€.
* main threadμμλ μλ°μ€ν¬λ¦½νΈ μ½λκ° μ€νλκ³ , web api threadμμλ μμ κ°μ ν¨μλ€μ΄ μ€νλλ€.
* μ΄ ν¨μλ€μ μ€νμ΄ λλλ©΄ callbackμ΄ callback queueμ μ½μλλ€.
* callback queueμ μ½μλ ν¨μλ€μ event loopμ μν΄ call stackμ μ½μλκ³  μ€νλλ€.


```JavaScript
console.log("log1");
setTimeout(() => {console.log("callback");}, 1000);
console.log("log2");
```
> μ€ν κ²°κ³Ό  
> log1   
> log2  
> callback   
> (callbackμ log2κ° μΆλ ₯λκ³  1μ΄ νμ μΆλ ₯λλ€.)

<img src="./img/process.jpeg" width="80%" alt="creation-phase">

> creation phaseμ call stackμ contextκ° μ½μλκ³  execution pahseμ μ€νλκ³  stackμμ μ­μ λλ κ³Όμ μ΄ λ°λ³΅λλ€.

* β   `console.log("log1")` μ€ν - "log1" μΆλ ₯
* β‘  `setTime()` ν¨μλ₯Ό μ€ννκΈ° μν thread μμ±
* β’  `console("log2")` μ€ν - "log2" μΆλ ₯
* β’  `setTimeout()` μ€ν - 1μ΄ κΈ°λ€λ¦Ό. **main threadκ° μλ μ€λ λμμ μ€νλκΈ°λλ¬Έμ 1μ΄λμ blockλμ§ μλλ€.**
* β£  1μ΄κ° μ§λ λ€ `console.log("callback")`μ΄ callback queueμ μ½μλλ€.
* β€  call stackμ΄ λΉμ΄μκΈ° λλ¬Έμ callback queueμ ν¨μκ° call stackμ μ½μλκ³  μ€νλλ€. - "callback" μΆλ ₯
