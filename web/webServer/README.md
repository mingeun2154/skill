# Web Server

> ### references ๐
> ์ํ์ฝ๋ฉ! HTML+CSS+์๋ฐ์คํฌ๋ฆฝํธ    
> ์ด๋ณด ์น ๊ฐ๋ฐ์๋ฅผ ์ํ ์คํ๋ง5    
> https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/dashboard    

## Contents		
* ### [์๋ฒ์ ํด๋ผ์ด์ธํธ](https://github.com/mingeun2154/skill/tree/main/web/webServer#server-and-client)      
* ### [์น ์ปจํ์ธ ](https://github.com/mingeun2154/skill/tree/main/web/webServer#web-content)      
* ### [Web Server](https://github.com/mingeun2154/skill/tree/main/web/webServer#web-server-2)      
* ### [WAS](https://github.com/mingeun2154/skill/tree/main/web/webServer#wasweb-application-server)      
* ### [Servlet](https://github.com/mingeun2154/skill/tree/main/web/webServer#servlet-1)

#    

## Server and Client
server๋ **์๋น์ค๋ฅผ ์ ๊ณตํ๋ ์ฌ๋**, client๋ **๊ณ ๊ฐ**์ด๋ผ๋ ๋ป์ด๋ค.

์น์ด๋ ์ธํฐ๋ท์ ํตํด HTML ๋ฌธ์๋ฅผ ์ฃผ๊ณ ๋ฐ๋ ๊ธฐ์ ์ด๋ค. 

์ธํฐ๋ท์ ์ฐ๊ฒฐ๋ PC๋ค ์ค ์น ํ์ด์ง์ ๊ฐ์ **์์์ ์์ฒญํ๋ PC๋ฅผ ํด๋ผ์ด์ธํธ**, **์ ๊ณตํ๋ PC๋ฅผ ์๋ฒ**๋ผ๊ณ  ํ๋ค.

## Web Content
์น ์๋ฒ๊ฐ ํด๋ผ์ด์ธํธ์๊ฒ ์ ๊ณตํ๋ ์น ์ปจํ์ธ ์๋ ๋ ๊ฐ์ง ์ข๋ฅ๊ฐ ์๋ค. 

* static content : server๊ฐ disk์ ์๋ ํ์ผ์ **๊ทธ๋**๋ก ๋ฐํํ๋ค.

* dynamic content : **executable file์ ์คํํ์ฌ ๊ทธ ๊ฒฐ๊ณผ**๋ฅผ ํด๋ผ์ด์ธํธ๋ก ์ ๋ฌํ๋ค.

## Web Server
web server๋ผ๊ณ  ํ๋ฉด ์ผ๋ฐ์ ์ผ๋ก **static content๋ฅผ ์ ๊ณต**ํ๋ ํ๋ก๊ทธ๋จ์ ๋งํ๋ค.

๋ํ์ ์ผ๋ก Apache Server, NginX ๋ฑ์ด ์๋ค.

**์น ์๋ฒ๋ ์ค์น๋ PC์ ํน์  port๋ฅผ listeningํ๊ณ  ์๋ค๊ฐ http request๊ฐ ๋์ฐฉํ๋ฉด ๊ทธ๊ฒ์ ์ฒ๋ฆฌํ๋ ํ๋ก๊ทธ๋จ์ผ๋ก ์ ๋ฌํ๋ค.**

์น ์๋ฒ๋ server-side program์ด ์คํ๋  ํ๊ฒฝ์ ์ ๊ณตํ  ๋ฟ์ด๋ค. 

server-side program์ DB ์ฐ๊ฒฐ, transaction ์ฒ๋ฆฌ ๋ฑ์ ๊ธฐ๋ฅ์ ๊ฐ์ถ๊ณ  ์๋ค.

## WAS(Web Application Server)
Web container, **Servlet Container**๋ผ๊ณ ๋ ํ๋ค.

> ~ container๋ ์ผ๋ฐ์ ์ผ๋ก ~๊ฐ ์คํ๋๋ **ํ๊ฒฝ**์ ์ ๊ณตํ๋ ์ํํธ์จ์ด์ด๋ค.    
> ๊ฐ์ฒด๋ค์ life-cycle์ ๊ด๋ฆฌํ๊ณ  ๊ฐ์ฒด๋ฅผ ์ฌ์ฉํ  ์ ์๋ API๋ฅผ ์ ๊ณตํ๋ค.    

๋ํ์ ์ผ๋ก Tomcat, JBoss, Jeus ๋ฑ์ด ์๋ค.

๋์  ์ปจํ์ธ ๋ฅผ ์ ๊ณตํ๊ธฐ ์ํ **ํ๊ฒฝ**์ ์ ๊ณตํ๋ค.

* ์คํ๋ง๊ณผ WAS

<img src="./img/spring.jpeg" width="70%" alt="์คํ๋ง๊ณผ was">

> WAS๋ฅผ ์คํ์ํค๊ณ , WAS๊ฐ ์ธ์ํ๋ ์ง์ ๋ ์์น์ .jar ํ์ผ์ ๋๋ฉด ์๋ฒ์์ ์ ํ๋ฆฌ์ผ์ด์์ด ์คํ๋๋ค.     
> ๋ฟ๋ง ์๋๋ผ WAS์์ ์คํ๋  Servlet์ ๋ํ ์ค์ (web.xml)๋ ๋ฐ๋ก ํด์ค์ผ ํ๋ค.     

* ์คํ๋ง ๋ถํธ์ WAS

<img src="./img/spring-boot.jpeg" width="70%" alt="์คํ๋ง ๋ถํธ์ was">

> spring boot application์ ์คํ์ํค๋ฉด ๋ณ๋์ ์ค์  ์์ด ํฐ์บฃ ๋ด์ฅ์๋ฒ๊ฐ ์คํ๋๊ณ  spring container๊ฐ ์คํ๋๋ค.    
> spring์ ๋นํด ๊ต์ฅํ ๊ฐ๋จํ๋ค. ๋ณต์กํ ์ค์  ์์ด ์๋น์ค ๊ฐ๋ฐ์๋ง ์ง์คํ  ์ ์๋ค.	

## Servlet
Java EE ํ์ค ๊ธฐ์  ์ค ํ๋์ด๋ค. java.servlet ํจํค์ง์ ์ ์๋์ด์๋ ํด๋์ค๋ค์ด๋ค.

servlet์ ์ฌ์ฉํ๋ฉด socket, input/outputstream ๋ฑ์ ์ ๊ฒฝ ์ฐ์ง ์์๋ ๋๋ค.

* Java SE(Standard Edition) : ๊ฐ์ฅ ๊ธฐ๋ณธ์ด ๋๋ ํ๋ซํผ. java.lang, java.io, java.util ๋ฑ์ ํจํค์ง๋ฅผ ํฌํจํ๋ค.
* Java EE(Enterprise Edition) : Java SE ์์ ๊ตฌ์ถ๋ ํ๋ซํผ. **๋คํธ์ํฌ ์ ํ๋ฆฌ์ผ์ด์์ ๊ฐ๋ฐ, ์คํํ๊ธฐ ์ํ API์ ํ๊ฒฝ**์ ์ ๊ณต.
