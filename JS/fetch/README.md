# Fetch API

simple description  

> ### references ๐

## Contents		
* ### [Fetch API](https://github.com/mingeun2154/skill/tree/main/JS/promise#promise-2)      
* ### [subheading](#)      

#    

## Fetch API
fetch๋ ์๋ฐ์คํฌ๋ฆฝํธ๊ฐ ์ ๊ณตํ๋ ๋ฉ์๋์ด๋ค. API ์๋ฒ๋ก **http ์์ฒญ์ ์ก์  ๋ฐ ์์ ํ  ์ ์๋๋ก ๋์์ค๋ค.**

`fetch()` ํจ์๋ `Promise`๊ฐ์ฒด๋ฅผ ๋ฐํํ๋ค. ๋ฐ๋ผ์ `then()`์ ํตํด ์ฝ๋ฐฑ์ ์ ๋ฌํด ์๋ต์ ์ฒ๋ฆฌํ  ์ ์๋ค.

`catch()` ๋ฉ์๋๋ฅผ ์ฌ์ฉํด์ **rejected case**์ ๋ํ ์ฝ๋ฐฑ์ ์ง์ ํ  ์๋ ์๋ค. 

> ### ๐จ `catch()`๋ฅผ ์ฌ์ฉํ ๋ ์ฃผ์ํ  ์ 
> 
> Fetch API์ Promise๋ **๋คํธ์ํฌ ์ค๋ฅ** ๋๋ **CORS ์ค๋ฅ**์ ๋ํด์๋ง TypeError๋ฅผ ๋ฐ์์ํค๊ณ  rejectํ๋ค.    
> 
> ํํ ๋ณผ ์ ์๋ 404 error๋ ๋คํธ์ํฌ ์ค๋ฅ๋ ์๋๋ฏ๋ก `catch()`๋ก๋ handleํ  ์ ์๋ค. 

`fetch()`ํจ์๋ JSONย ์ ๋ฐ๋ก ๋ฐํํ์ง ์๊ณ  `Response`**๊ฐ์ฒด๋ฅผ resolveํ๋** `Promise`**๊ฐ์ฒด๋ฅผ ๋ฐํํ๋ค.**

`Response`๊ฐ์ฒด๋ JSON body๊ฐ ์๋ **entire HTTP response**๋ฅผ ๋ฐํํ๋ค.

`Response.json()`๋ฉ์๋๋ JSON ํํ์ text๋ฅผ **JavaScript object**๋ก parsingํ๊ณ  **์ด ๊ฐ์ฒด๋ฅผ ๊ฐ์ธ๋ `Promise`๋ฅผ ๋ฐํ**ํ๋ค.

### example 

<img src="./img/fetch-example.png" width="80%" alt="fetch-example">

* `Promise.reject(reason)` - reject๋ `Promise`๋ฅผ ๋ฐํํ๋ค.
* `Response.ok` - HTTP ์๋ต์ state code๊ฐ 200~299๋ฉด true, ์๋๋ฉด false์ด๋ค.
* `Promise.catch()` - rejected `Promise`์ ๋ํ ์ฝ๋ฐฑ์ ๋ฑ๋กํ๋ค. **์ต์ข์ ์ผ๋ก Promise๋ฅผ ์ ๋ฌ๋ฐ๋๊ณณ์์ ํธ์ถํ๋ค.** 

<img src="./img/catch.png" width="50%" alt="catch">
