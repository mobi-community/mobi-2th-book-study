##### | 모던 자바스크립트 DeepDive <br />

###### range: 49. Babel과 Webpack을 이용한 ES6+/ES.NEXT 개발 환경 구축 <br />

###### date: day32 (2024.02.29) <br />

<hr />
<br />

### babel

바벨은 ES6+/ES.NEXT로 구현된 최신 사양의 소스코드를 구형 브라우저에서도 동작하는 ES5 사양의 소스코드 변환(트랜스파일링)이 가능. <br />

#### install babel

```javascript
// 프로젝트 폴더 생성
$ mkdir esnext-project && cd esnext-project
// package.json 생성
$ npm init -y
// babel-core, babel-cli 설치
$npm install --save-dev @babel/core @babel/cli
```

```javascript
// package.json
{
    "name": "esnext-project",
    "version" : "1.0.0",
    "devDependencies" : {
        "@babel/cli": "^7.10.3",
        "@babel/core": "^7.10.3"
    }
}
```

Babel과 Webpack, 플러그인의 버전은 빈번하게 업그레이드된다. <br />
`npm install`은 언제나 최신 버전의 패키지를 설치하므로 특정 버전으로 설치하고 싶은 경우 패키지 이름 뒤에 @과 설치하고 싶은 버전을 지정하면 된다.

```javascript
npm install --save-dev @babel/core@7.10.3 @babel/cli@7.10.3
```

<br />

#### babel preset 설치

바벨을 사용하려면 `@babel/preset-env`를 설치해야 한다. <br />
`@babel/preset-env`는 함께 사용돼야 하는 바벨 플러그인을 모아둔 것으로 Babel preset이라 부른다.

```javascript
// babel preset
1. @babel/preset-env
2. @babel/preset-flow
3. @babel/preset-typescript
```

`@babel/preset-env`는 필요한 플러그인ㅇ들을 프로젝트 지원 환경에 맞춰 동적으로 결정해준다. 프로젝트 지원 환경은 Browserslist 형식으로 `.browserslistrc` 파일에 상세히 설정 가능하다. 이 작업을 생략할 경우 기본값으로 설정된다.

```javascript
// install @babel/preset-env
$ npm install --save-dev @babel/preset-env
```

<br />

#### babel.config.json 설정 파일 작성

설치가 완료되면 프로젝트 루트 폴더에 `babel.config.json` 설정 파일을 생성하고 아래와 같이 작성한다. (@babel/preset-env를 사용하겠다는 의미)

```javascript
// babel.config.json
{
    "presets":["@babel/preset-env"]
}
```

<br />

#### 트랜스파일링

npm scripts에 babel cli 명령어를 등록해두는 편이 비교적 덜 번거롭다.
package.json의 scripts를 추가하면 아래와 같이 된다.

```javascript
// package.json (final)
{
    "name": "esnext-project",
    "version" : "1.0.0",
    "scripts": {
        "build": "babel src/js -w -d dist/js"
    },
    "devDependencies" : {
        "@babel/cli": "^7.10.3",
        "@babel/core": "^7.10.3",
        "@babel/preset-env": "^7.10.3"
    }
}
```

npm scripts의 build는 src/js 폴더(타겟 폴더)에 있는 모든 자바스크립트 파일들을 트랜스파일링 후 결과물을 dist/js 폴더에 저장한다. 사용한 옵션의 의미는 아래와 같다.

- `-w` <br />
  --watch 옵션의 축약형. <br />
  타겟 폴더에 있는 모든 자바스크립트 파일들의 변경을 감지해 자동으로 트랜스파일. <br />

- `-d` <br />
  --out-dir 옵션의 축약형. <br />
  트랜스파일링된 결과물이 지정될 폴더를 지정. <br />
  만약 지정된 폴더가 존재하지 않으면 자동 생성. <br />

<br />

#### babel 플러그인 설치

babel 플러그인 중에서 public/private 클래스 필드를 지원하는 `@babel/plugin-proposal-class-properties`를 설치하자.

```javascript
npm install --save-dev @babel/plugin-proposal-class-properties
```

설치 후 플러그인은 `babel.config.json` 설정 파일에 추가해야 한다.

```javascript
// babel.config.json
{
    "presets":["@babel/preset-env"],
    "plugins":["@babel/plugin-proposal-class-properties"],
}
```

<br />

### Webpack

webpack은 의존 관계에 있는 자바스크립트, css, 이미지 등의 리소스들을 하나 또는 여러 개의 파일로 번들링하는 모듈 번들러다. <br />
webpack을 사용하면 의존 모듈이 하나의 파일로 번들링되므로별도의 모듈 로더가 필요 없다. <br />
그리고 여러 개의 자바스크립트 파일을 하나로 번들링하므로 HTML 파일에서 script 태그로 여러 개의 자바스크립트 파일을 로드해야 하는 번거로움도 사라진다.

#### install webpack

```javascript
$ npm install --save-dev webpack webpack-cli
```

<br />

#### install babel-loader

webpack이 모듈을 번들링할 때 babel을 사용해 ES6+/ES.NEXT 사양의 소스코드를 ES5 사양의 소스코드로 프탠스파일링하도록 babel-loader를 설치한다.

```javascript
$ npm install --save-dev babel-loader
```

<br />

#### webpack.config.json 설정 파일 작성

`webpack.config.json`는 webpack이 실행될 때 참조하는 설정 파일이다. 프로젝트 루트 폴더에 `webpack.config.json`파일을 생성하고 아래와 같이 작성한다.

```javascript
// webpack.config.json

const path = require("path");

module.exports = {
  // entry file
  entry: "./src/js/main.js",
  // 번들링 된 js 파일의 이름과 저장될 경로 지정
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "js/bundle.js",
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        include: [path.resolve(__dirname, "src/js")],
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
          options: {
            presets: ["@babel/preset-env"],
            plugins: ["@babel/plugin-proposal-class-properties"],
          },
        },
      },
    ],
  },
  devtools: "source-map",
  mode: "development",
};
```

<br/>

#### install babel-polyfill

babel을 사용해 트랜스파일링해도 브라우저가 지원하지 않는 코드가 남아 있을 수 있다. `src/js/main.js`를 다음과 같이 수정해 ES6에서 추가된 Promise, Object.assign, Array.from 등을 트랜스파일링 할려면 @babel/polyfill을 설치해야 한다.

```javascript
$ npm install @babel/polyfill
```

`@babel/polyfill`은 개발 환경에서만 사용하는 것이 아니라 실제 운영 환경에서도 사용해야 하므로 개발 의존성으로 설치하는 --save-dev 옵션을 지정하지 않는다.
