
## 1. NPM

### 프론트 엔드 개발에 Nodejs가 필요한 이유
- 1. 최신 스펙 개발 가능  
- Babel, Typescipt, SASS 사용하려면 트랜스 파일러 필요  

- 2. 빌드 자동화
- 파일 압축, 코드 난독화 등  

- 3. 개발환경 커스터 마이징  
- CRA 툴 있지만 각자의 사정에 맞는 환경에선 Node.js 지식이 필요  

### 패키지 관리  

NPM은 유의적버전(semantic version)을 따른다.
- eg) react:"^16.12.0"  
- 주 버전 Major Version : 16    -> 기존 버전과 호환되지 않게 변경한 경우
- 부 버전 Minor Version : 12    -> 기존 버전과 호환되면서 기능이 추가된 경우
- 수 부전 Patch  Version : 0     -> 기존 버전과 호환되면서 버그를 수정한 경우  

### 버전의 범위 관리
case1 ) 버전을 직접 명시  
- eg) npm install react:16.0.12  

case2 ) 부등호 버전 명시  
- eg) npm install react>=16.0.12  

case3 ) ~ 틸드 버전 명시  

- 마이너 버전이 명시되어 있으면, 패치버전만 변경한다.  
- eg) ~16.0.12 -> 16.0.0 부터 16.1.0 미만 까지 업데이트 가능  


- 마이너 머전이 명시가 없으면, 마이너 버전을 갱신  
- eg) ~0 -> 0.0.0 부터 1.0.0 미만을 포함


case4 ) ^ 버전 명시 --- ✔ 지금 사용하는 방법  
- 정식버전(1.0 이상) 에서는 마이너와 패치 버전을 변경한다.  
- eg) ^16.0.2 는 16.0.0 ~ 17.0.0 미만 

- 정식버전 아래애서는 , 패치버전만 변경한다.   
- eg) ^0.1.2 은  0.1.0 ~ 0.2.0 미만  
- * 마이너는 하위 호환성을 보장하는 규율이 있지만, 정식버전 아래에선 해당되지 않기 때문  

- eg)   "react": "~0" ->  "version": "0.14.10"    
- eg)   "react": "^0.0" ->  "version": "0.0.3"  
- 패치 버전만 변경하면서 설치가 된다. (1.0 이하)  


# 2. Webpack

## 2.1 웹팩이 필요한 이유

배경  
- 모듈시스템이 없어서, 전역 변수들이 오염될 가능성이 있음  
- 즉시실행함수를 이용해서 함수 스코프로 감싸 모듈을 만들었다.  

### 👨‍💻 IIFE immidiately invoked function expression  
- 실습  
### 👨‍💻 es_module  
- 실습  

type = module 을 모든 브라우저가 지원하지 않기 때문에  
웹팩을 통해 JS 을 번들링 한다.  

## 2.2 엔트리,아웃풋

webpack 실행하기  
- npm install -D webpack webpack-cli  
- 노드모듈스 폴더 안에 .bin 안에 실행파일들이 설치된다.  
- CLI 명령어를 사용할 수 있게 된다.  

webpack 옵션   
--mode development | prodcution | none  
--entry ./src/app.js
--output dist/main.js

### 👨‍💻 3_webpack_cli
npx webpack --mode development --entry ./src/app.js -o dist


### 👨‍💻 4_webpack_config  

```js
const path = require("path");

module.exports = {
  mode: "development",
  entry: {
    main: "./src/app.js", // entry point가 여러개일 수 있다.
    main2: "./src/app2.js",
  },
  output: {
    path: path.resolve("./dist"),
    filename: "[name].js", // entry포인트가 여러개인 경우 name 변수를 동적으로 할당해준다.
  },
};
// 실행 명령어
// 1. npx webpack
// script : "build":"webpack"
```
### 👨‍💻 4_webpack_config - 실습




## ref
- 강의  
https://www.inflearn.com/course/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD/lecture/31727?tab=curriculum

- 블로그  
https://jeonghwan-kim.github.io/series/2019/12/09/frontend-dev-env-npm.html

- 깃허브  
https://github.com/jeonghwan-kim/lecture-frontend-dev-env