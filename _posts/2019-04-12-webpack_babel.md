---
layout: post
title: react를 통한 기본적인 webpack과 babel 사용법.
permalink: posts/webpack-babel
tag: javascript react webpack babel
---

> 해당 포스트는 [Webpack, Babel, and React from Scratch — BUT WHY?](https://hackernoon.com/webpack-babel-and-react-from-scratch-but-why-889a385ff32f)를 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

저(필자)는 졸업 후 자바스크립트 생태계에대해서 많은 공부를 했습니다. react를 좋아하는 사람으로써 create-react-app에 대한 호기심이 생겼습니다. `npm install -g create-react-app`으로 가장 있기있는 react start pack을 설치할 수 있습니다. 근데 create-react-app이 어떻게 동작하는지 궁금해보신적 있으신가요? 혹은 어떻게 브라우저에서 빠르게 동작하는 앱을 적은 네트워크 요청으로 만들 수 있는지 궁금한 적이 있나요? 어떻게 `npm run build`이후에 빌딩하고 정적인 파일을 생성하는지? 이런 것들은 흥미롭습니다. 이런 마법같은 베일 아래 오픈소스 프로젝트에서 우리가 학습할 수 있도록 간소화된 코드를 제공해주고 있습니다.

저(필자)는 webpack과 babel 도움으로 react 어플리케이션을 만들고 Netlify로 배포하기로 결정했습니다. [깃허브 레포](https://github.com/jsphbtst/react-webpack-simple)에서 코드확인이 가능하며, 배포된 사이트는 [여기](https://agitated-hoover-cdafcd.netlify.com/)에 확인 가능합니다.

이 프로젝트는 버튼을 클릭했을 때 배경색이 변경되는 간단한 react 어플리케이션입니다. 우선 머릭속에 어떤 모습일지 상상해보세요. 우리는 클래스 베이스 컴포넌트가 필요할까요? 아님 함수형 컴포넌트가 필요할까요? onClick시 무엇을 해야할까요? state가 필요할까요?

이런 것들을 곰곰히 생각하고 있을 때 webpack과 babel을 세팅할 시간이 되었습니다. 여러분의 기기에 Node가 설치되었다는 가정하에 아래 명령문을 입력하시면 됩니다. 아래 명령문은 새로운 폴더를 만들고 이름을 react-webpack-simple이라고 칭하고 `npm init`을 하시면 됩니다. 계속해서 아래의 라이브러리를 설치하시면 됩니다.

```
mkdir react-webpack-simple
cd react-webpack-simple
npm init
npm install --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader
mkdir src
cd src
touch index.html index.js
cd ..
```

babel-core는 ES2015+ 코드를 호환 가능한 자바스크립트 하위버전으로 변경해줍니다. @babel/preset-env와 @babel/preset-react는 babel과 react를 기능을 지원하는 플러그인입니다. 이것들은 뒷단에서 큰 역할을 합니다. 마지막으로 babel-loader는 우리가 설정한 방법대로 자바스크립트 코드를 변환합니다.

루트 디렉토리로 이동한 다음, 우리의 경우 react-webpack-simple가 루트 디렉토리입니다. 여기서 .babelrc 라는 파잉을 만들어 줍니다. 이 파일은 앞으로 우리의 바벨을 어떻게 사용할지 설정을 하는 곳입니다. 위에 언급했던 것과 같이 @babel/preset-env와 @babel/preset-react을 작성합니다.

```javascript
// .babelrc 파일
{
  "preset": ["@babel/preset-env", "@babel/preset-react"]
}
```

좋습니다! 우리는 프로젝트에서 가장 어려운부분을 조금씩 해결해가고 있습니다. 다음에 루트 디렉토리에 webpack.config.js 파일을 만들어 봅시다. 이것은 webpack의 환경설정을 하는 파일입니다. webpack은 모듈 번들러입니다. 각기 다른 프로젝은 다른 목표를 가지고 있고 다른 방법으로 서버파일이 필요할 수 있습니다. html파일에 하나의 css 파일을 스타일태그를 가지기를 원한다면? 캐싱이 가능하게하기 바란다면, 앞으로 마법이 펼쳐질겁니다.

먼저 webpack은 몇 개의 코어 컨셉을 가지고 있고 그 부분과 친숙해져야합니다. 코어 컨셉은 [도큐먼트](https://webpack.js.org/concepts/)에서 확인할 수 있습니다. Entry는 webpack이 내부 의존성 그래프를 빌딩하는 엔트리포인트입니다. 우리의 경우 아무 것도 임포트받지 않아서 `./src/index.js` 그래프 일부에 속하지 않습니다. 여러분은 자바스크립트 파일과 다른 것들은 적절하게 임포트를 받아야 합니다. output은 webpack이 생성하는 모든 번들이 생성되는 곳입니다. webpack이 자바스크립트와 JSON만 이해할 수 있기 때문에 이미지나 css 파일 그리고 다른 것들을 이해하기 위해서는 함수 혹은 미들웨어가 있어야 합니다. 이런 미들웨어는 loader에 의해 정해지며 webpack은 이러한 미들웨어를 활용해 자바스크립트나 JSON파일이 아닌것들을 이해하고 의존성을 고려해 적절한 곳에 파일을 위치시킵니다. 마지막으로 plugins은 번들링 프로세스와 자산관리 그 밖에 다른 것을 하면서 로더를 서포트합니다.

```javascript
// webpack.config.js 파일을 사용하기전에 의존성을 주입해야합니다.
npm install --save-dev html-webpack-plugin mini-css-extract-plugin react react-dom
```

아래의 webpack.config.js은 위에 이론을 적용한 어플리케이션입니다. VENDOR_LIBS는 우리가 만들 react 어플리케이션안에 사용할 모든 라이브러리가 포함되어 있습니다. 필요한 모든 라이브러리를 로드하는 것을 원치않기 때문에 이런한 배열을 만들었습니다.

[name].[chunkhash].bundle.js 포맷은 캐싱을 위한 프로세스입니다. UX를 개선하기위해서 사이트를 로드할때마다 필요한 것들을 매번 다운로드하는걸 원하지 않습니다. 의존성이 캐시되면 유저들이 이미 의존성을 다운받았기때문에 재 방문을 하면 로딩이 빠른 속도로 됩니다. 업데이트를 한다고해도 새로운 버전에 필요한 부분만 다운로드를 하고 모든 소스를 다운로드하지는 않습니다.

```javascript
const path = require("path");
const webpack = require("webpack");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

const VEBDOR_LIBS = ["react", "react-dom"];

module.export = {
  entry: {
    bundle: "./src/index.js",
    vendor: VENDOR_LIBS
  },
  output: {
    path: path.join(__dirname, "dist"),
    filename: "[name].[chunkhash].bundle.js",
    chunkFilename: "[name].[chunkhash].bundle.js"
  },
  optimization: {
    splitChunks: {
      cacheGroups: {
        vendor: {
          chunks: "initial",
          name: "vendor",
          test: "vendor",
          enforce: true
        },
      }
    },
    rentimeCheck: true
  },
  module: {
      rules: [
          {
              test: \/.js$/,
              exclude: /node_modules/,
              use: {
                  loader: 'babel-loader'
              }
          },
          {
              test:\/.html$/,
              use:{
                  loader:'html-loader'
              }
          },
          {
              test: \/.css$/,
              use: [
                  MiniCssExtractPlugin.loader,
                  'css-loader'
              ]
          }
      ]
  },
  plugins: [
      new HtmlWebpackPlugin({
          template: './src/index.html'
      }),
      new MiniCssExtractPlugin({
          filename: '[name].css',
          chunkFilename:'[id].css'
      }),
      new webpack.DefinePlugin({
          'process.env.NODE_ENV': JSON.stringify(process.env.NODE_ENV)
      })
  ]
};
```

module 섹션에서 babel-loader는 자바스크립트 코드를 변환하는데 사용됩니다. 자바스크립트가 아닌 파일은 어떻게 처리한다고 이야기했는지 기억나시나요? HTML과 CSS파일은 자바스크립트가 아니기때문에 html-loader와 css-loader를
이용해 처리를 합니다. test는 파일이 [insert extension here]으로 끝나면 webpack은 [inset loader here]을 사용할 겁니다. 예를 들어 파일이름이 html으로 끝나면 webpack은 html-loader을 이용한다는 뜻입니다.

plugin 섹션에는 HtmlWebpackPlugin은 HTML 도큐먼트에서 자바스크립트 파일을 임포트하는데 사용합니다. 프로젝트가 빌드될 때마다 스크립트 태그의 이름을 업데이트하는것은 성가신 일입니다. MiniCssExtractPlugin은 여러개의 CSS 파일을 하나의 자바스크립트파일로 생성해주는 기능을 합니다. webpack.DefinePlugin은 프로젝트가 생성될 수 있도록 도와줍니다. 리엑트에서는 생산과 개발이 다르게 동작됩니다.

마지막으로 해야할 webpack 환경설정은 rimraf와 webpack-dev-server를 npm을 통해 설치하는 겁니다. rimraf는 기존 빌드된 파일을 지우고 새로운 파일은 생성해주는 라이브러리입니다. 이러한 방법으로 오래된 파일과 새로운 파일이 혼재되는 것을 방지할 수 있습니다. webpack-dev-server는 개발환경에서 사용하는데 코드가 변경될 때마다 자동적으로 브라우저가 리로드될 수 있게 만들어 프로젝트를 빌드할때마다 index.html 파일을 여는 번거로움을 막아줍니다. 또한 아래와 같이 package.json파일을 수정하세요. `npm run dev`는 빌드 파일을 생성하고 `npm run start`는 개발서버를 생성할 겁니다.

```javascript
// npm install --save-dev rimraf webpack-dev-server 를 먼저 실행하시는 것을 잊지 마세요.
"script": {
    "clean": "rimraf dist",
    "start": "webpack-dev-server --open --mode development",
    "build": "NODE_ENV=production npm run clean && webpack -p"
}
```

코드를 작성한 후에 폴더 구조는 아래 이미지와 같을 겁니다. dist 폴더가 빌드된 파일을 가지고 있습니다. 이 폴더는 `npm run build`할때 자동으로 생성됩니다.

![react-webpack-simple folder directory image](https://cdn-images-1.medium.com/max/800/1*55Ec7_AqGajbOaNBulCfVg.png)

index.html 파일은 아래와 같은 코드를 포함하고 있습니다.

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="utf-8">
        <link rel="stylesheet" href="http://maxcdn.bootstrapcdn.com/bootstrap/latest/css/bootstrap.min.css">
        <title>리엑트, 웹핵, 바벨 </title>
    </head>
    <body>
        <div id="root"><div>
    </body>
</html>
```

create-react-app를 사용해 봤다면 div 태그는 root id가 있다는 것이 익숙할 겁니다. 여기서는 react에대해서 가르치는 자리가 아니고 프레임워크에 대한 사용법을 어느정도 안다는 가정하에 이야기를 하고 있습니다. 아래 react코드를 사용할 예정입니다. bootstarp 3을 사용하고 있고 4개의 버튼이 랜더링 되고 각 버튼을 클릭하면 각기 다른 배경색으로 변경됩니다.

```javascript
import React, { Component } from "react";
import ReactDOM from "react-dom";
import "../style/style.css";

class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      changer: true
    };
  }

  componentDidMount() {}

  render() {
    return (
      <div className="App">
        <h1>Tester</h1>
        <p>{this.state.changer + ""}</p>
        <button
          className="btn"
          onClick={() => this.setState({ changer: !this.state.changer })}
        >
          State Change
        </button>
        <div className="row">
          <div className="col-xs-12 col-sm-6 col-md-3 col-lg-3">
            <button
              className="btn"
              onClick={() => {
                document.body.style.backgroundColor = "#ed6a5a";
              }}
            >
              ed6a5a
            </button>
          </div>
          <div className="col-xs-12 col-sm-6 col-md-3 col-lg-3">
            <button
              className="btn"
              onClick={() => {
                document.body.style.backgroundColor = "#fbfffe";
              }}
            >
              fbfffe
            </button>
          </div>
          <div className="col-xs-12 col-sm-6 col-md-3 col-lg-3">
            <button
              className="btn"
              onClick={() => {
                document.body.style.backgroundColor = "#f6a90a";
              }}
            >
              f6a90a
            </button>
          </div>
          <div className="col-xs-12 col-sm-6 col-md-3 col-lg-3">
            <button
              className="btn"
              onClick={() => {
                document.body.style.backgroundColor = "#9bc1bc";
              }}
            >
              9bc1bc
            </button>
          </div>
        </div>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById("root"));
```

긴 과정이지만 노력할만한 가치가 있습니다. 터미널로 가서 `npm run build`를 입력하고 엔터를 누르면 dist 폴더에 있는 index.html을 브라우저에 드래그앤 드롭을 하면 됩니다! Netlify를 통해서 프로젝트를 배포했습니다.
