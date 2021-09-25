# Babel


### 바벨 목적  
- 브라우저마다 스펙이 달라, JS코드는 동일하게 작동하지 않을 수 있다.
- 크로스 브라우징 이슈를 해결해 주는것이 바벨이다.
- ECMAScript2015+,Typescript,JSX 등 다른언어를 포함하여 모든 브라우저에서 동작하도록 하는것이 목표


### 트랜스 파일 vs 빌드  
- 추상화 수준이 다른 변환은 빌드
- 트랜스 파일은 추상화수준이 같다. (TS->JS,JSX->JS) 이므로 여전히 코드를 읽을 수 있다.

### 바벨의 단계

1. 파싱 Parsing : 토큰화 이후 추상 구문 트리 (AST) 로 변환
2. 변환 Transforming : AST를 변환 (eg) const -> var로)
3. 출력 Printing : 파일로 출력


## 바벨 설치 

```
// 바벨 코어, 명령어를 위한 cli 설치
npm install -D @babel/core  @babel/cli
```

## 바벨 실행 

```
// 바벨 실행
>npx babel app.js
const alert = msg => window.alert(msg);

// 바벨 실행 + 플러그인
npx babel app.js --plugins ./myplugin.js
```
## 플러그인

### 플러그인 - 커스텀 플러그인 작성

커스텀 플러그인 작성    
eg) 식별자를 출력하고, 뒤집어주는 플러그인
```js
// myplugin.js:
module.exports = function myplugin() {
  return {
    visitor: {
      Identifier(path) {
        const name = path.node.name;

        // 바벨이 만든 AST 노드를 출력한다
        console.log("Identifier() name:", name);

        // 변환작업: 코드 문자열을 역순으로 변환한다
        path.node.name = name.split("").reverse().join("");
      },
    },
  };
};

```

eg) const 를 var로 바꿔주는 플러그인
```js
// myplugin2.js:
module.exports = function myplugin() {
  return {
    visitor: {
      // https://github.com/babel/babel/blob/master/packages/babel-plugin-transform-block-scoping/src/index.js#L26
      VariableDeclaration(path) {
        console.log("VariableDeclaration() kind:", path.node.kind); // const

        if (path.node.kind === "const") {
          path.node.kind = "var";
        }
      },
    },
  };
};

```


### 플러그인 -  @babel 플러그인 

```js
npm install -D @babel/plugin-transform-block-scoping
npm install -D @babel/plugin-transform-arrow-functions
npm install -D @babel/plugin-transform-strict-mode

// const -> var 로 변환해주는 등 블록 스코프>함수 스코프로 변환
npx babel app.js --plugins @babel/plugin-transform-block-scoping

// 화살표 함수 변환 추가
npx babel app.js --plugins @babel/plugin-transform-block-scoping --plugins @babel/plugin-transform-arrow-functions

// 설정파일 추가 후 
npx babel app.js
```
👨‍💻 01_plugin

## 프리셋


### 커스텀 프리셋

@babel/프리셋을 따로 파일로 만들어서 babel설정파일에 넣을 수 있다.

```js
// mypreset.js
module.exports = function mypreset() {
  return {
    plugins: [
      "@babel/plugin-transform-arrow-functions",
      "@babel/plugin-transform-block-scoping",
      "@babel/plugin-transform-strict-mode",
    ],
  }
}
```

```js
// babel.config.js
module.exports = {
  presets: ["./mypreset.js"],
}
```
👨‍💻 02_custom_preset

### @babel 프리셋

프리셋을 다운 받아 설정파일에 넣으면   
지금까지 했던 설정을 한번에 할 수 있다.  
>npm install -D @babel/preset-env

```js
// babel.config.js:
module.exports = {
  presets: ["@babel/preset-env"],
}
```
👨‍💻 03_babel_preset