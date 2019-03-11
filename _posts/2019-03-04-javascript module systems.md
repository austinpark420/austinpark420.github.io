---
layout: post
title: javascript module systems
permalink: posts/javascript_module_systems
tag: javascript
---

> 해당 포스트는 [JavaScript Module Systems Showdown: CommonJS vs AMD vs ES2015](https://auth0.com/blog/javascript-module-systems-showdown/)을 번역한 글입니다. 오역한 부분이 있으면 댓글 부탁드립니다.

- 자바스크립트 개발이 점점 보편화되고 의존성 등을 다루기가 어려워지고 있습니다. 이러한 문제를 해야하기 위해 모듈시스템이 개발되었습니다. 이 글에서는 우리는 현재 개발자들이 문제를 해결하기위해 사용하는 여러 솔류션과 그 문제를 살펴보려고 합니다.

## 자바스크립트 모듈은 왜 필요할까요?

- 만약에 개발 플랫폼에 익숙하다면, 의존성과 캡슐화에 대한 개념을 알고 있을 겁니다.이전에 존재했던 소프트웨어들은 각각의 소프트웨어들은 특정한 조건이 만족되기 전까지 고립된 상태로 개발되었습니다. 새로운 소프트웨어를 프로젝트로 도입할 때 해당 소프트웨어와 새로운 소프트웨어 사이에 의존성이 생겨납니다. 함께 동작하기위해서 서로 출동이 발생하지 않게하는 것이 중요합니다. 별것 아닌 이야기처럼 들리겠지만 캡슐화 없이 두 모듈이 충동하는 것은 시간 문제입니다.

- 캡슐화는 다른 코드와 충돌을 방지하기위해 필수적입니다.
  클라이언트 사이드 자바스크립트 의존성은 절대적입니다. 즉, 개발자는 코드가 실행되었을 때 의존성을 유지하는게 중요한 업무입니다. 또한 의존성이 정상적으로 동작하도록 하는것도 중요한 일입니다.
  아래의 코드는 Backbone.js의 일부분입니다. 스크립트는 지시사항대로 정확하게 동작합니다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Backbone.js Todos</title>
    <link rel="stylesheet" href="todos.css" />
  </head>

  <body>
    <script src="../../test/vendor/json2.js"></script>
    <script src="../../test/vendor/jquery.js"></script>
    <script src="../../test/vendor/underscore.js"></script>
    <script src="../../backbone.js"></script>
    <script src="../backbone.localStorage.js"></script>
    <script src="todos.js"></script>
  </body>

  <!-- (...) -->
</html>
```

- 자바스크립트 개발은 점점 더 복잡해지고 있습니다. 의존성을 다루는 것은 성가신 일입니다. 리팩토링한 코드도 손상됩니다. 새로운 의존성을 주입할 때 어디에 코드를 삽입해야 이전의 코드가 동작되는 순서를 유지할 수 있을까요?

- 자바스크립트 모듈은 이런 문제와 그 밖에 것들을 다룹니다. 그들은 점점 더 커지는 자바스크립트를 컨드롤하기위해 생겼습니다. 이제 다양한 솔루션에 대해서 알아 봅시다.

## An Ad-Hoc Solution: 리빌링 모듈 패턴

- 대부분의 모듈 시스템은 최신입니다. 모듈 시스테이 존재하기 전, 특정 프로그램 패턴이 많은 자바스크립트 코드에 사용되었습니다. 이것이 리빌링 모듈 패턴입니다.

```javascript
var myRevealingMoudle = (function() {
  var privateVar = "Yongmin Park",
    publicVar = "Hello !";

  function privateFunction() {
    conosle.log("Name: " + privateVar);
  }

  function publicSetName(strName) {
    privateVar = strName;
  }

  function publicGetName() {
    privateFunction();
  }

  // 퍼블릭은 프라이빗 함수와 프로퍼티를 가르킨다.
  return {
    setName: publicSetName,
    greeting: publicVar,
    getName: publicGetName
  };
})();

myRevealingModule.setName("austin Park");
```

> 위에 예시는 [Addy Osmani's JavaScript Design Patterns](https://addyosmani.com/resources/essentialjsdesignpatterns/book/)를 참고한 내용입니다.

- 자바스크립트 스코프(ES2015 let으로 가정)는 함수레벨 스코프가 있습니다. 즉,함수 내에서 바인딩된 무엇이든 함수 외부로 벗어날 수 없습니다. 이러한 이유로 드러나는 모듈패턴은 프라이빗 컨텐츠를 캡슐화하는데 함수를 사용합니다.(다른 자바스크립트 패턴처럼)

위에 예시처럼, return 안에 있는 public 심볼은 노출되고, 다른 선언문은 함수 스코프안에 감싸집니다. 프라이빗 범위를 감싸는 함수에 대해 var 혹은 즉시 실행 함수를 사용할 필요도 없습니다. 그리고 기명함수는 모듈로 사용될 수 있습니다.

이 패턴은 자바스크립트 프로젝트에서 자주 사용되고 캡슐화 문제와고 잘 어울리지만 의존성 문제와는 크게 상관이 없습니다.

### 장점

- 어디에서든 구현하기 간편합니다.(라이브러리와 다른 언어의 도움 없이)
- 하나의 파일에 여러 모듈을 정의할 수 있습니다.

### 단점

- 프로그램적으로 모듈을 임포트할 방법이 없습니다.
- 의존성은 지시사항대로 다뤄져야 합니다.
- 비동기 모듈 로딩이 불가능합니다.
- 순환 종속성에 문제가 있을 수 있습니다.
- 정적 코드기로 분석하기 어렵습니다.

## CommonJS

CommonJS는 서버사이드 자바스크립트 어플리케이션을 개발하는 데 도움이 되는 사양을 정의하기 위한 프로젝트입니다. CommonJS팀이 해결하려고 시도한 것 중 하나가 모듈입니다. Node.js 개발자들이 CommonJS 사양을 따르려고 했지만 나중에 반대했습니다. Node.js는 구현에 있어서 모듈에 많은 영향을 받습니다.

```javascript
// In circle.js
exports.area = r => 2 * PI * r * r;

exports.circumference = r => 2 * PI * r;

// In some file
const circle = require("./circle.js");
console.log(`The area of a circle of radius $ is ${circle.area(4)}`);
```

-

Node.js 모듈 시스템 상단에 Node.js와 CommonJS의 갭을 연결하는 라이브러리 형태로 추상화라는 개념이 있습니다. 해당 포스트를 위해 오직 동일한 기본 기능을 보여줄 것입니다.

Node.js와 CommonJS 모듈 모두 필수적으로 *require*과 _export_ 2개의 element가 있습니다. *require*는 다른 모듈에서 현재의 스코프로 심볼을 임포트하는 함수힙니다. *require*에 전달된 파라미터는 모듈의 id입니다. 노드 구현에 있어서 _node_moudle_ 디렉토리에 안에 있는 이름으로 사용됩니다.(디렉토리안에 있지 않다면, 그 디렉토리의 경로입니다.) *exports*는 특별한 객체입니다. 어떤 것이든 그 안에 넣으면 pubulic element으로 익스포트 됩니다. 필드의 이름이 보존됩니다. Node.js와 CommonJS에 독특한 차이점은 *module.exports*객체 형태에서 발생합니다. Node.js의 *module.exports*는 실제 익스포트된 객체이고, *exports*는 module.exports에 바인딩된 변수입니다. 반면에 CommonJS는 module.expots 객체가 아닙니다. 이는 Node.js는 미리 만들어진 객체를 module.exports없이 익스포트를 할 수 없다는 뜻입니다.

```javascript
// 아래의 코드를 동작하지 않습니다. exports로 대체되면 module.exports에 바인딩이 사라집니다.
exports = width => {
  return {
    area: () => width * width
  };
};

// 아래의 코드는 실행됩니다.
module.exports = width => {
  return {
    area: () => width * width
  };
};
```

CommonJS 모듈은 서버개발자 측면에서 설계되었습니다. 자연스럽게 API는 동기식입니다. 즉, 모듈들은 필요한 순간에 로드되고 순서대로 로드됩니다.

### 장점

- 개발자는 문서를 보지 않고 개념을 알 수 있습니다.
- 종속성 관리를 통합시겼습니다. 모듈은 다른 모듈을 요청하고 필요한 순서대로 로드됩니다.
- *require*은 어디서든 호출할 있습니다. 모듈은 프로그래밍방식으로 로드됩니다.
- 순환 종속성이 지원됩니다.

### 단점

- 동기식 API는 특정 상황에 적합하지 않을 수 있습니다.(clinet-side)
- 모듈당 하나의 파일입니다.
- 브라우저는 로드 라이브러리나 트랜스파일링이 필요합니다. \*\*\*
- 모듈에 대한 생성자함수가 없습니다. \*\*\*
- 정적 코드기로 분석하기 어렵습니다.

### Implementations

- 우리는 이미 Node.js 구현에 대해서 이야기를 나눴습니다.
- 클라이언트 사이드를 위한 webpark과 browserify라는 2가지 옵션이 있습니다. Browserify는 노드 모듈과 유사한 모듈을 파스하기위해 개발되었고, 의존성이 포함된 모듈을 하나의 파일로 번들링합니다. 반면에 Webpack은 게시 전에 소스변환의 복잡한 파이프라인를 핸들링하기 위해서 만들어졌습니다. 여기에는 CommonJS 모듈을 번들로 묶는 것도 포함됩니다.

## Asynchronous Module Definition (AMD)

- AMD는 CommonJS에 불만을 가진 개발자 집단에서 만들어졌습니다. 사실 AMD 개발 초기에는 CommonJS 개발과 분리되어 있었습니다. AMD와 CommonJS에 가장 큰 차이는 비동기 모듈 로딩을 지원입니다.

```javascript
// 의존성 배열과 factory 함수로 define 호출
define(["dep1", "dep2"], function(dep1, dep2) {
  // 반환값으로 모듈값을 정의
  return function() {};
});

// 혹은
define(function(require) {
  var dep1 = require("dep1"),
    dep2 = require("dep2");

  return function() {};
});
```

비동기식 로딩은 자바스크립트의 전통적인 클로저 관용구를 사용할 수 있게 합니다. 요청된 모듈은 로딩이되면 함수가 호출됩니다. 모듈 정의 그리고 모듈 임포팅은 동일한 함수로 실행됩니다. 모듈이 정의되면 그것들의 의존성은 명시적으로 만들어집니다. 그러므로 AMD로더는 완벽한 의존성 그래프의 완전한 그림을 주어진 프로젝트 런타임에서 가질 수 있습니다. 서로 의존하지 않는 라이브러리는 동시에 로드될 수 있습니다. 이것은 특히 시간 단축이 필수적인 브라우저에서 중요합니다.

### 장점

- 비동기식 로딩을 지원합니다.
- 순환 의존성 지원합니다.
- require과 exports의 적합성합니다. \*\*\*
- 통합적인 의존성 관리에 용이합니다.
- 여러개의 파일로 모듈 분리 가능합니다.
- 생성자함수 지원합니다.
- 플러그인 지원합니다

### 단점

- 문법적 복잡합니다.
- 트랜스파일이 되어있지 않다면 로더 라이브러리 필요합니다.
- 정적 코드기로 분석하기 어렵습니다.

### Implementations

- 현재 가장 유명한 AMD로 구현한 것은 require.js와 Dojo입니다.
- require.js를 사용하는 것은 매우 간다합니다. HTML파일에 라이브러리를 포함하고 data-main 어트리뷰트를 이용해 어떤 모듈을 먼저 로드할지 require.js에게 알려줍니다. Dojo도 비슷한 설정을 가지고 있습니다.

## ES2015 Module

- 다행히도, ECMA 팀은 모듈 이슈를 해결하기위해 나서기로 결정합니다. 그 결과는 자바스크립트 스탠다드에서 볼 수 있습니다. 그 결과는 문법적으로 동기와 비동기 모두 호환 됩니다.

```javascript
// lip.js
export const sqrt = Math.sqrt;
export function square(x) {
  return x * x;
}

export function diag(x, y) {
  return sqrt(squart(x) + square(y));
}

// main.js
import { square, diag } from "lib";
console.log(square(11));
console.log(diag(4, 3));
```

- _import_ 디렉티브는 네임스페이스에서 모듈을 사용하는데 사용될 수 있습니다. 반대로 이 디렉티브는 require과 define과 달리 동적은 아닙니다. 반면 export 디렉티브는 퍼블릭으로 사용할 수 있도록 만들 수 있습니다.

- *import*와 _export_ 디렉티브는 정적인 특성으로 인해 정적 분석기는 코드를 실행하지 않고도 전체 종속성 트리를 작성 할 수 있습니다. ES2015는 모듈의 동적로드를 지원하지 않지만 초안 스펙은 다음을 수행합니다.

```javascript
System.import("some_module")
  .then(some_module => {
    // 모듈 사용
  })
  .catch(error => {
    //
  });
```

> ES2015는 정적 모듈로더에 대해서만 저정합니다. 실제로 ES2015 구현은 파싱이후에 아무것도 할 필요가 없습니다. System.js와 같은 모듈 로도가 여전히 필요합니다. 브라우저 모듈 로더에 대한 초안을 사용할 수 있습니다.

- 이런한 솔류션은 언어에 통합되어 있기 때문에 런타임에 모듈로딩에 대한 가장 적합한 전략을 세울 수 있습니다. 즉, 비동기 로딩을 런타임에 활용할 수 있습니다.

> 2017/02 업데이트: 지금은 동적 모듈 로딩이 가능합니다. 이것은 ECMAScript 사양에 명시되어 있습니다.

### 장점

- 동기와 비동기 로딩을 모두 지원합니다.
- 문법이 간결합니다.
- 정적 분석도구를 지원합니다.
- 라이브러리가 필요없고 어디서든 사용이 가능합니다.
- 순환 의존성을 지원합니다.

### 단점

- 지원하는 곳이 없습니다.

### Implementations

- 불행히도 주요 라바스트립트 런타임은 ES2015 모듈을 지원하지 않습니다. 이러한 의미는 파이어폭스, 크롬, Node.js가 모듈을 지원하지 않는다는 것 입니다. 다행히도 만은 트랜스파일러가 모듈을 지원하고 있고, 폴리필도 가능합니다. 바벨은 위한 ES2015 사전설정으로 문제없이 모듈을 다루고 있습니다.

## System.js

- 모듈시스템을 사용해서 레가시 코드에서 벗어나려고 시도할 수 있습니다. 또는 무슨 일이 있어도 당신이 선택한 솔류션이 동작하기를 바랄 수 있습니다. CommonJs, AMD, ES2015 모듈을 지원하는 System.js를 사용하십시오. 바벨 또는 트레이서와 같이 트랜스파일러와 함께 동작할 수 있으며 Node 와 IE8+ 환경을 지원합니다.

```javascript
<script src="system.js"></script>
<script>
  //  baseURL 참조 경로 설정
  System.config({
    baseURL: '/app',
    // 'traceur' 혹은 'typescript'
    transpiler: 'babel',

    // traceurOptions 혹은 typescriptOptions
    babelOptions: {

    }
  });

  // loads /app/main.js
  System.import('main.js');
</script>
```

- System.js는 모든 일을 바로 하기때문에, ES2015 모듈은 프로덕션 모드가 빌딩을 하는 동안에 트랜스파일러에 남아있어야 합니다. 프로덕션 모드가 아닌 경우, System.js는 프로덕션과 디버깅환경을 자연스럽게 전환할 수 있도록 트랜스파일러를 호출할 수 있습니다.

---
