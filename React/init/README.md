# Start React Project

프론트엔드 개발 환경 설정.
> ### references 🔗    
> React.js, 스프링 부트, AWS로 배우는 웹 개발 101

## Contents		
* ### [Node.js](#)      
* ### [패키지 관리](#)      
* ### [프로젝트 초기화](#)      

#    

## Node.js
Node.js는 JavaScript가 실행되는 **환경**(runtime)이다.

Node.js가 생기기 전에는 JavaScript는 웹 브라우저에서만 실행되었다.

Node.js는 구글 Chrome의 V8이라는 JavaScript engine을 실행한다.

JavaScript를 웹 브라우저 밖에서 실행할 수 있다는 것은 클라이언트 뿐만 아니라 **서버를 만들 수 있다**는 뜻이다.

## NPM(Node Package Manager)
Node.js의 패키지(dependency=라이브러리) 관리 시스템이다.

Gradle이 mvn repository에서 라이브러리를 다운받는 것과 비슷하다.

NPM을 이용해 [npmjs](https://www.npmjs.com)에서 Node.js 라이브러리를 설치한다.

node 프로젝트의 dependencies는 node_modules 디렉토리에 설치된다.

## 프로젝트 초기화
`$ npm init`

> node 프로젝트를 초기화(package.json이 생성된다.)

`$ npx init` 

> 여러 가지 설정을 건너뛸 수 있다.

`$ npm install react` 

> 리액트(라이브러리) 설치

`$ npm install` 

> package.json 파일에 명시된 dependencies를 모두 설치한다.

`$ npx create-react-app [앱 이름]` 

> 리액트 애플리케이션 설치

`$ npm start`

> 애플리케이션 실행
