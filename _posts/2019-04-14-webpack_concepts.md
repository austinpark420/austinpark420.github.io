---
layout: post
title: webpack의 코어 컨셉
permalink: posts/webpack
tag: javascript webpack
---

> 해당 포스트는 [Webpack concepts](https://webpack.js.org/concepts/)를 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

webpack에서 가장 중요한 것은 모던 자바스크립트 어플리케이션을 위해 모듈을 번들링하는 것입니다. 어플리케이션에서 webpack이 동작할 때 내부적으로 [의존성 그래프](https://webpack.js.org/concepts/dependency-graph/)를 생성합니다. 이것은 프로젝트에 필요한 모든 모듈을 묶고 하나 혹은 그 이상의 번들을 생성합니다.

> 자바스크립트 모듈과 webpack모듈에 대해서 더 알고 싶다면 [여기](https://webpack.js.org/concepts/modules/)를 참고하세요.

ver4.0.0이후 webpack에서 프로젝트를 번들링하기위해서 더는 환경설정파일이 필요없어 졌습니다. 그렇지만 그것은 [당신의 필요](https://webpack.js.org/configuration/)로 사용할 수 있습니다.

webpack을 시작하기위해서 그것의 코어 컨셉에대해서 알아야합니다.

- [Entry](#Entry)
- [Output](#Output)
- [Loader](#Loader)
- [Plugins](#Plugins)
- [Mode](#Mode)
- [Browser Compatibility](#BrowserCompatibility)

이 도큐먼트는 코어 개념을 제공하고 있고, 좀 더 자세한 내용이 궁금하면 아래의 링크를 참조하시기 바랍니다.

이는 모듈 번들러와 그들이 어떻게 동작하고 리소스를 어떻게 다루는지에 대한 내용이 나왔습니다.

- [어플리케이션 번들링 메뉴얼](https://www.youtube.com/watch?v=UNMkLHzofQI)
- [모듈 번들러의 라이브코딩](https://www.youtube.com/watch?v=Gc9-7PBqOC8)
- [간단한 모듈 번들러의 상세한 설명](https://github.com/ronami/minipack)

<a name="Entry"></a>

## Entry

엔트리 포인트는 webpack이 내부 의존성그래프를 빌딩하기위해 장소를 가르킵니다. webpack은 다른 모듈과 라이브러리가 엔트리 포인트를 참고하는 특징이 있습니다.

기본값은 ./src/index.js이지만 entry의 프로퍼티값을 변경함으로 엔트리 포인트를 변경할 수 있습니다.

webpack.config.js

```javascript
module.export = {
  entry: "./path/to/my/entry/file.js"
};
```

> [엔트리포인트](https://webpack.js.org/concepts/entry-points/) 자세하기 알아보기

<a name="Output"></a>

## Output

output 프로퍼티는 webpack이 번들링한 파일을 어디에 저장하고 파일이름을 어떻게 할지 설정합니다. ./dist/main.js가 파일이 아웃풋되는 디폴트 값이고, ./dist에 다른 파일들이 생성됩니다.

output 필드의 환경설정을 변경해서 디폴트값을 변경할 수 있습니다.

webpack.config.js

```javascript
const path = require("path");

module.export = {
  entry: "./path/to/my/entry/file.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "my-first-webpack.bundle.ejs"
  }
};
```

위에 예시에서 우리는 output.filename과 output.path 프로퍼티로 webpack에게 번들링될 이름과 위치를 지시했습니다. 이러한 경우 경로 모듈이 루트에 임포트되는지 궁금할 수 있습니다. 이것은 핵심 [Node.js 모듈](https://nodejs.org/api/modules.html)이 파일경로를 조작하는데 사용됩니다.

> output 프로퍼티는 [더 많은 환경설정 기능](https://webpack.js.org/configuration/output/)이 있도 만약 컨셉에 대해서 좀 더 자세히 알고 싶다면 [output 세션](https://webpack.js.org/concepts/output/)을 읽어보는 것을 추천드립니다.

<a name="Loader"></a>

## Loader

webpack은 자바스크립트와 JSON만 이해할 수 있습니다. Loader는 webpack이 다른 종류의 파일을 처리하고 어플리케이션에서 사용할 수 있는 [유효한 모듈](https://webpack.js.org/concepts/modules/)로 변환시키고 의존성 그래프에 추가시킵니다.

> css와 같이 다른 타입을 모듈을 입포트하는 능력은 webpack의 기능이며 다른 모듈번들러나 테스크 러너가 제공하지 않습니다. 이런 언어의 확장은 개발자가 좀 더 정확한 의존성 그래프를 만드는데 보증할 수 있습니다.

loader는 webpack 환경설정에서 2개의 프로퍼티를 가지고 있습니다.

1. test 프로퍼티는 어떤 파일을 변경해야하는지 가르킵니다.
2. use 프로퍼티는 어떤 loader가 변환을하는데 사용하는지 가르킵니다.

webpack.config.js

```javascript
const path = require('path')
module.export = {
  output: {
    filename: 'my-first-webpack.bundle.js'
  },
  module: {
    rules: [
      {test: \/.txt$/, use: 'row-loader'}
    ]
  }
};
```

위에 환경설정은 rules 프로퍼티를 test, use를 사용하기위해서 정의했습니다. 이것은 webpack의 컴파일러에게 다음과 같이 알려줍니다.

"require()/import 구문에서 '.txt'파일은 만나면 번들에 추가하기전에 raw-loader을 사용해서 변경을 해라."

> webpack 환경설정을 할때 ruels가 아니라 module.rules에 정의한다는 것은 중요합니다. 잘못 설정을 하면 webpack에서 경고를 합니다.

> 파일 매치를 위해 정규식을 사용할 때 특정 인용부로를 사용할 수 없습니다. 예를 들어 \/.txt$/은 '/\.txt$/'/ "/\.txt\$/"와 동일하지 않습니다. 전자는 webpack에 끝이 .txt으로 끝나는 파일을 매치시키고 후자는 webpack에 .txt파일만 매치시킵니다.

loader에 대해서 더 많은 내용일 궁금하면 [loader 섹션](https://webpack.js.org/concepts/loaders/)을 읽어보시길 추천드립니다.

<a name="Plugins"></a>

## Plugins

loader가 특정의 타입을 모듈을 변화하는 사용하는 반면, plugins는 자산 매니지먼트 환경변수의 주입 등 번들 최척화하는 것같이 광범위하게 사용될 수 있습니다.

> [plugin interface](https://webpack.js.org/api/plugins/)을 확인하고 webpack에서 어떻게 확장해서 사용할지 알아보세요.

plugin을 사용하기 위해 require()이 필요하고 plugins 배열을 추가해야합니다. 모든 plugins는 옵션을 통해 커스터마이징이 가능합니다. 다른 목적으로 plugin을 여러번 사용한다면 new 오퍼레이터를 이용해 호출함으로써 인스턴스를 생성할 수 있습니다.

webpack.config.js

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin'); // npm을 통해서 설치 필요
const webpack = requrie('webpack'); // 빌트 인 plugins 접근

module.export = {
  module: {
    rules: [
      {test: \/.txt$, use: 'raw-loader'}
    ]
  },
  plugin: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
```

위에 예시에서 html-webpack-plugin은 어플리케이션에서 자동적으로 모든 번들을 주입하여 HTML파일을 생성합니다.

> 다양한 plugin을 확인하기위해서 [pluins 리스트](https://webpack.js.org/plugins/)를 확인 해보세요.

<a name="Mode"></a>

## Mode

mode 파라미터를 developmnet, production, none으로 설정합니다. 각각의 환경 응답으로 webpack 빌트인 최적화를 사용할 수 있습니다. 디폴트 값은 production 입니다.

```javascript
module.export = {
  mode: "production"
};
```

[mode 환경설정](https://webpack.js.org/configuration/mode/)에 대해서 더 많이 알아보세요.

<a name="BrowserCompatibility"></a>

## Browser Compatibility

webpack은 [ES5가 호환](https://kangax.github.io/compat-table/es5/)되는 모든 브라우저를 지원합니다.(IE8 이하는 지원하지 않습니다.) webpack은 import()와 require.ensure()을 위해 promise가 필요합니다. 만약 좀 더 오래된 브라우저를 지원하고 싶다면 [폴리필](https://webpack.js.org/guides/shimming/)이 필요합니다.
