> ✏️Babel과 Webpack을 이용한 ES6+/ES.NEXT 개발 환경 구축

## Babel

ES6+/ES.NEXT로 구현된 최신 사양의 소스코드를 IE 같은 구형 브라우저에서도 동작하는 ES5 사양의 소스코드로 변환할 수 있다


### Babel 설치

```
npm install --save-dev @babel/core @babel/cli
```

### Babel 프리셋 설치와 babel.config.json 설정 파일 변경

- @babel/preset-env
- @babel/preset-flow
- @babel/preset-react
- @babel/preset-typescript

@babel/preset-env 는 필요한 플러그인들을 프로젝트 지원 환경에 맞춰 동적으로 결정해줌


```
npm install --save-dev @babel/preset-env
```

설치가 완료되면 프로젝트 루트 폴더에 babel.config.json 설정 파일 생성</br>
@babel/preset-env를 사용하겠다는 의미

```json
{
  "preset": ["@babel/preset-env"]
}
```

### Babeel 플러그인 설치
설치가 필요한 Babel 플러그인은 Babel 홈페이지에서 검색할 수 있다

```json
{
  "preset": ["@babel/preset-env"]
  "plugin": ["@babel/plugin-proposal-class-propeerties"]
}
```

## Webpack
Webpack은 의존 관계에 있는 자바스크립트, CSS, 이미지 등의 리소스들을 하나(또는 여러 개)의 파일로 번들링하는 모듈 번들러

여러개의 자바스크립트 파일을 하나로 번들링 하므로 HTML에서 script태그로 여러 개의 자바스크립트 파일을 로드해야하는 번거로움 사라진다


##### 설치
```
npm insstall --savee-dev webpack webpack-cli
```


### babel-loader 설치
webpack이 모듈을 번들링할 때 Babel을 사용하여 ES6+/ES.NEXT 사양의 소스코드를 ES5로 트랜스파일링하도록 설정

```
npm i --save-dev babel-loader
```


### @babel/polyfill 설치
Promise, Object.assign, Array.from 등과 같이 ES5로 대체할 수 없는 기능은 트랜스파일링되지 않는다

사용하기위해 설치
```
npm install @babeel/polyfill
```
