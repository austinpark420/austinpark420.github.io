---
layout: post
title: 초보자를 위한 웹팩(Webpack) 소개
permalink: posts/Abeginner’sIntroductionToWebpack
tag: webpack
---

> 해당 포스트는 [A beginner’s introduction to Webpack
> ](https://medium.com/free-code-camp/a-beginners-introduction-to-webpack-2620415e46b3)를 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

## 웹팩(webpack)이란 무엇인가?

웹팩은 자바스크립트 모듈을 컴파일할 수 있는 툴로서 모듈 번들러로 알려져 있습니다.

여러개의 파일이 주어지면 앱을 실행하는 하나(혹은 여러개의) 파일로 변환해 줍니다.

웹팩은 많은 기능을 수행합니다.

- 리소스를 묶어주는 역할
- 변화를 감지해서 업무를 다시 실행
- 바벨을 활용해 ES5으로 코드 변환, 브라우저와 상관없이 최신 자바스크립트 기능을 사용할 수 있게 해줌
- 커피스크립트를 자바스크립트로 컴파일
- 인라인 이미지를 데이터 URIs으로 변환
- CSS 파일을 임포트할 수 있음
- 개발 웹서버를 실행시킬 수 있음
- 핫 모듈을 대신해서 사용할 수 있음
- 첫 화면이 로드될 때 큰 자바스크립트 파일이 불려지는 것을 피하기위해 출력 파일을 여러개로 나눌 수 있음
- tree shaking을 만들 수 있음

웹팩은 프론트 뿐만 아니라 백엔드에서 유용하게 사용될 수 있습니다.

웹팩과 비슷한 기능을 수행하는 것들은 많습니다. 가장 큰 차이점은 그러한 도구들은 테스크러너로 알려져 있고, 웹팩은 모듈 번들러입니다.

웹팩이 도구에 더 초점이 맞춰져 있습니다. 단지 앱에서 엔트리 포인트(스크립트가 포함되어 있는 HTML 파일일 수 있습니다)를 지정해주면 되고 웹팩은 파일을 분석해 앱을 실행할 수 있도록 하나의 자바스크립트 파일로 만들어 줍니다.

## 웹팩 인스톨

프로젝트에 따라 웹팩은 글로벌 혹은 로컬로 설치할 수 있습니다.

### 글로벌로 설치하기

yarn을 활용해 웹팩 글로벌로 설치하기

    yarn global add webpack webpack-cli

npm 으로 설치하기

    npm i -g webpack webpack-cli

설치를 완료하면, 코드를 실행할 수 있습니다.

    webpack-cli

### 로컬로 설치하기

웹팩은 로컬로도 설치가 가능합니다. 로컬이 권장하는 설치방법이며 그 이유는 웹펙이 프로젝트별로 업데이트될 수 있고 의존성을 줄일 수 있는 방법입니다.

Yarn으로 설치하기

    yarn add webpack webpack-cli -D

npm으로 설치하기

    npm i webpack webpack-cli --save-dev

설치를 완료하면, package.json 파일에 아래 코드를 삽입해야 합니다.

    {
    	//...
    	"scripts": {
    		"build": "webpack"
    	}
    }

코드 삽입을 완료하면 웹팩을 프로젝트 루트에서 실행시킬 수 있습니다.

    yarn build

## 웹팩 환경설정

기본적으로 웹팩 버전 4 이후에는 아래 규칙을 준수하는 경우 환경설정이 필요없습니다.

- 프로젝트 엔트리 포인트가 ./src/index.js
- 출력은 ./dist/main.js
- 웹팩은 프로덕션 모드에서 동작

물론 필요하다면 웹팩 설정을 변경할 수 있습니다. 웹팩 환경설정은 프로젝트 루투의 webpack.config.js에 저장되어 있습니다.

## 엔트리 포인트

기본적으로 엔트리 포인트는 ./src/index.js이며, 해당 예제에서는 ./index.js파일은 엔트리 포인트로 설정했습니다.

    module.export = {
    	/*...*/
      entry: './index.js'
      /*...*/
    }

## 출력

기본적으로 출력은 ./dist/main.js이지만 해당 예제에서는 app.js으로 설정했습니다.

    module.exports = {
      /*...*/
      output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'app.js'
      }
      /*...*/
    }

웹팩을 사용한다는 것은 자바스크립트 뿐만 아니라 CSS같은 파일에서도 import나 require을 사용할 수 있다는 것을 의미합니다.

웹팩은 자바스크립트, 로더 뿐만 아니라 모든 의존성을 컨트롤하는 것을 목표로 하고 있습니다.

예를 들어 당신의 코드에서 아래와 같이 사용할 수 있습니다.

    import 'style.css'

이는 로더 환경설정을 통해서 가능합니다.

정규식은 모든 CSS 파일을 대상으로 합니다.

    module.exports = {
      /*...*/
      module: {
        rules: [
          { test: /\.css$/, use: 'css-loader' },
        }]
      }
      /*...*/
    }

로더는 옵션을 가질 수 있습니다.

    module.exports = {
      /*...*/
      module: {
        rules: [
          {
            test: /\.css$/,
            use: [
              {
                loader: 'css-loader',
                options: {
                  modules: true
                }
              }
            ]
          }
        ]
      }
      /*...*/
    }

각 요구사항마다 여러개의 로더가 필요할 수 있습니다.

    module.exports = {
      /*...*/
      module: {
        rules: [
          {
            test: /\.css$/,
            use:
              [
                'style-loader',
                'css-loader',
              ]
          }
        ]
      }
      /*...*/
    }

위에 예제에서는 css-loader는 CSS에서 import 'style.css'를 해석하고 style-loader는 <style>태그를 사용하여 DOM에 해당 CSS를 삽입합니다.

순서가 중요하고 마지막부터 먼저 실행됩니다.

로더 종류는 무엇이 있을까요? 아주 많습니다. [링크참조](https://webpack.js.org/loaders/)

일반적으로 사용되는 로더로는 바벨이 있으며 자바스크립트 파일을 ES5코드로 변환해줍니다.

    module.exports = {
      /*...*/
      module: {
        rules: [
          {
            test: /\.js$/,
            exclude: /(node_modules|bower_components)/,
            use: {
              loader: 'babel-loader',
              options: {
                presets: ['@babel/preset-env']
              }
            }
          }
        ]
      }
      /*...*/
    }

아래 예제는 바벨이 모든 리엑트/JSX 파일을 전처리하도록 합니다. ([바벨옵션 보기](https://webpack.js.org/loaders/babel-loader/))

    module.exports = {
      /*...*/
      module: {
        rules: [
          {
            test: /\.(js|jsx)$/,
            exclude: /node_modules/,
            use: 'babel-loader'
          }
        ]
      },
      resolve: {
        extensions: [
          '.js',
          '.jsx'
        ]
      }
      /*...*/
    }

## 플러그인

플러그인은 로더와 비슷하지만 스테로이드에 있습니다. 로더가 할 수 없는 것을 할 수 있으며, 웹팩에서 중요한 부분입니다.

    module.exports = {
      /*...*/
      plugins: [
        new HTMLWebpackPlugin()
      ]
      /*...*/
    }

HTMLWebpackPlugin 플러그인은 HTML파일은 자동적으로 생성하고 자바스크립트 번들 위치에 추가를 합니다. ([다양한 플러그인 보기](https://webpack.js.org/plugins/))

유용한 플러그인으로는 CleanWebpackPlugin가 있으며 출력을 하기 전에 dist/ 폴더를 지웁니다.

    module.exports = {
      /*...*/
      plugins: [
        new CleanWebpackPlugin(['dist']),
      ]
      /*...*/
    }

## 웹팩 모드

웹팩 4에서 소개된 모드는 각 웹팩이 동작하는 환경을 설정합니다. development 혹은 production으로 설정할 수 있으며 디폴트값은 production입니다. 그래서 development 환경이 필요할 때 설정을 하면 됩니다.

    module.exports = {
      entry: './index.js',
      mode: 'development',
      output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'app.js'
      }
    }

Development mode

- 매우 빠른 빌드
- 프로덕션보다 덜 최적화
- 코멘트를 삭제하지 않음
- 좀 더 자세한 에러 메세지와 수정 사안 제안
- 좀 더 효율적인 디버깅 환경

Production 모드는 최적화를 위해 빌드되는 데 좀 더 시간이 소요됩니다. 좀 더 작은 자바스크립트 파일이 출력되며 production에서 불필요한 내용을 제거됩니다.

샘플 앱을 만들어서 콘솔을 찍어봤습니다.

production 번들
![production](https://miro.medium.com/max/2692/0*dOY4LO-A9pkCwVUq.png)

development 번들

![development](https://miro.medium.com/max/2800/0*T6Ug7GCoAp_gCv3X.png)

## 웹팩 실행시키기

글로벌로 설치했을 경우, CLI 메뉴얼대로 실행할 수 있습니다. 만약 package.json에 스크립트로 삽입되어 있다면 npm 혹은 yarn으로 실행시켜야 합니다.

아래 예시와 같이 package.json에 스크립트가 정의되어 있다면

npm run build 혹은 yarn run build(혹은 yarn build)으로 웹팩을 실행시켜야 합니다.

    "scripts": {
      "build": "webpack"
    }

## 변화 감지

웹팩은 앱 변화가 감지되면 자동으로 다시 빌드되고 다음 변화를 기다립니다

아래 스크립트를 추가하는 것만드로도 가능합니다.

그리고 npm run watch 혹은 yarn run watch(혹은 yarn watch)를 실행시켜주면 됩니다.

    "scripts": {
      "watch": "webpack --watch"
    }

watch모드의 좋은 기능 중 하나는 빌드 에러가 없을 경우에 빌드된다는 것입니다. 에러가 있다면 watch는 변화를 기다리며 다시 빌드를 시도합니다. 그리고 현재 번들에 영향을 주지 않습니다.

## 이미지 핸들링

웹팩은 file-loader 로더로 이미지를 매우 효율적으로 사용할 수 있게 해줍니다.

환경설정은 아래와 같이 간단합니다.

    module.exports = {
      /*...*/
      module: {
        rules: [
          {
            test: /\.(png|svg|jpg|gif)$/,
            use: [
              'file-loader'
            ]
          }
        ]
      }
      /*...*/
    }

자바스크립트에서 아래와 같이 이미지를 import할 수 있습니다.

    import Icon from './icon.png'

    const img = new Image()
    img.src = Icon
    element.appendChild(img)

위에 img는 HTMLLmageElement입니다. ([이미지 도큐먼트](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/Image))

file-loader는 fonts, CSV files, XML 등과 같이 다른 타입도 핸들링할 수 있습니다.

이미지와 함께 사용하기 좋은 로더는 url-loader입니다.

아래 로더 예시는 8KB 작은 PNG파일을 [data URL](https://flaviocopes.com/data-urls/)으로 로드합니다.

    module.exports = {
      /*...*/
      module: {
        rules: [
          {
            test: /\.png$/,
            use: [
              {
                loader: 'url-loader',
                options: {
                  limit: 8192
                }
              }
            ]
          }
        ]
      }
      /*...*/
    }

## SASS 코드를 CSS 파일로 변경하는 프로세스

sass-loader, css-loader, style-loader을 이용합니다.

    module.exports = {
      /*...*/
      module: {
        rules: [
          {
            test: /\.scss$/,
            use: [
              'style-loader',
              'css-loader',
              'sass-loader'
            ]
          }
        ]
      }
      /*...*/
    }

## 소스맵 생성

웹팩은 코드를 묶기 때문에 소스 파일은 오류를 일으킨 원본 파일에 대한 참조를 가져와야합니다.

devtool 속성을 사용해서 소스 맵을 생성하도록 웹팩에게 지시합니다.

    module.exports = {
      /*...*/
      devtool: 'inline-source-map',
      /*...*/
    }

devtool은 많은 값이 있으면 일반적으로 사용되는 값은 아래와 같습니다.

- none: 소스맵을 생성하지 않음
- source-map: production에서 사용하기 이상적이며, 최소화할 수 있는 별도의 소스 맵을 제공하고 번들에 참조를 추가하므로 개발 도구는 소스맵을 사용할 수 있는 것을 알고 있습니다. 디버깅 목적으로만 사용해야합니다.
- inline-source-map: development에서 사용하기 이상적으로 소스 맵을 DATA URL 인라인으로 표시합니다.

## 웹팩(webpack)이란 무엇인가?

웹팩은 자바스크립트 모듈을 컴파일할 수 있는 툴로서 모듈 번들러로 알려져 있습니다.

여러개의 파일이 주어지면 앱을 실행하는 하나(혹은 여러개의) 파일로 변환해 줍니다.

웹팩은 많은 기능을 수행합니다.

- 리소스를 묶어주는 역할
- 변화를 감지해서 업무를 다시 실행
- 바벨을 활용해 ES5으로 코드 변환, 브라우저와 상관없이 최신 자바스크립트 기능을 사용할 수 있게 해줌
- 커피스크립트를 자바스크립트로 컴파일
- 인라인 이미지를 데이터 URIs으로 변환
- CSS 파일을 임포트할 수 있음
- 개발 웹서버를 실행시킬 수 있음
- 핫 모듈을 대신해서 사용할 수 있음
- 첫 화면이 로드될 때 큰 자바스크립트 파일이 불려지는 것을 피하기위해 출력 파일을 여러개로 나눌 수 있음
- tree shaking을 만들 수 있음

웹팩은 프론트 뿐만 아니라 백엔드에서 유용하게 사용될 수 있습니다.

웹팩과 비슷한 기능을 수행하는 것들은 많습니다. 가장 큰 차이점은 그러한 도구들은 테스크러너로 알려져 있고, 웹팩은 모듈 번들러입니다.

웹팩이 도구에 더 초점이 맞춰져 있습니다. 단지 앱에서 엔트리 포인트(스크립트가 포함되어 있는 HTML 파일일 수 있습니다)를 지정해주면 되고 웹팩은 파일을 분석해 앱을 실행할 수 있도록 하나의 자바스크립트 파일로 만들어 줍니다.

## 웹팩 인스톨

프로젝트에 따라 웹팩은 글로벌 혹은 로컬로 설치할 수 있습니다.

### 글로벌로 설치하기

yarn을 활용해 웹팩 글로벌로 설치하기

    yarn global add webpack webpack-cli

npm 으로 설치하기

    npm i -g webpack webpack-cli

설치를 완료하면, 코드를 실행할 수 있습니다.

    webpack-cli

### 로컬로 설치하기

웹팩은 로컬로도 설치가 가능합니다. 로컬이 권장하는 설치방법이며 그 이유는 웹펙이 프로젝트별로 업데이트될 수 있고 의존성을 줄일 수 있는 방법입니다.

Yarn으로 설치하기

    yarn add webpack webpack-cli -D

npm으로 설치하기

    npm i webpack webpack-cli --save-dev

설치를 완료하면, package.json 파일에 아래 코드를 삽입해야 합니다.

    {
    	//...
    	"scripts": {
    		"build": "webpack"
    	}
    }

코드 삽입을 완료하면 웹팩을 프로젝트 루트에서 실행시킬 수 있습니다.

    yarn build

## 웹팩 환경설정

기본적으로 웹팩 버전 4 이후에는 아래 규칙을 준수하는 경우 환경설정이 필요없습니다.

- 프로젝트 엔트리 포인트가 ./src/index.js
- 출력은 ./dist/main.js
- 웹팩은 프로덕션 모드에서 동작

물론 필요하다면 웹팩 설정을 변경할 수 있습니다. 웹팩 환경설정은 프로젝트 루투의 webpack.config.js에 저장되어 있습니다.

## 엔트리 포인트

기본적으로 엔트리 포인트는 ./src/index.js이며, 해당 예제에서는 ./index.js파일은 엔트리 포인트로 설정했습니다.

    module.export = {
    	/*...*/
      entry: './index.js'
      /*...*/
    }

## 출력

기본적으로 출력은 ./dist/main.js이지만 해당 예제에서는 app.js으로 설정했습니다.

    module.exports = {
      /*...*/
      output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'app.js'
      }
      /*...*/
    }

웹팩을 사용한다는 것은 자바스크립트 뿐만 아니라 CSS같은 파일에서도 import나 require을 사용할 수 있다는 것을 의미합니다.

웹팩은 자바스크립트, 로더 뿐만 아니라 모든 의존성을 컨트롤하는 것을 목표로 하고 있습니다.

예를 들어 당신의 코드에서 아래와 같이 사용할 수 있습니다.

    import 'style.css'

이는 로더 환경설정을 통해서 가능합니다.

정규식은 모든 CSS 파일을 대상으로 합니다.

    module.exports = {
      /*...*/
      module: {
        rules: [
          { test: /\.css$/, use: 'css-loader' },
        }]
      }
      /*...*/
    }

로더는 옵션을 가질 수 있습니다.

    module.exports = {
      /*...*/
      module: {
        rules: [
          {
            test: /\.css$/,
            use: [
              {
                loader: 'css-loader',
                options: {
                  modules: true
                }
              }
            ]
          }
        ]
      }
      /*...*/
    }

각 요구사항마다 여러개의 로더가 필요할 수 있습니다.

    module.exports = {
      /*...*/
      module: {
        rules: [
          {
            test: /\.css$/,
            use:
              [
                'style-loader',
                'css-loader',
              ]
          }
        ]
      }
      /*...*/
    }

위에 예제에서는 css-loader는 CSS에서 import 'style.css'를 해석하고 style-loader는 <style>태그를 사용하여 DOM에 해당 CSS를 삽입합니다.

순서가 중요하고 마지막부터 먼저 실행됩니다.

로더 종류는 무엇이 있을까요? 아주 많습니다. [링크참조](https://webpack.js.org/loaders/)

일반적으로 사용되는 로더로는 바벨이 있으며 자바스크립트 파일을 ES5코드로 변환해줍니다.

    module.exports = {
      /*...*/
      module: {
        rules: [
          {
            test: /\.js$/,
            exclude: /(node_modules|bower_components)/,
            use: {
              loader: 'babel-loader',
              options: {
                presets: ['@babel/preset-env']
              }
            }
          }
        ]
      }
      /*...*/
    }

아래 예제는 바벨이 모든 리엑트/JSX 파일을 전처리하도록 합니다. ([바벨옵션 보기](https://webpack.js.org/loaders/babel-loader/))

    module.exports = {
      /*...*/
      module: {
        rules: [
          {
            test: /\.(js|jsx)$/,
            exclude: /node_modules/,
            use: 'babel-loader'
          }
        ]
      },
      resolve: {
        extensions: [
          '.js',
          '.jsx'
        ]
      }
      /*...*/
    }

## 플러그인

플러그인은 로더와 비슷하지만 스테로이드에 있습니다. 로더가 할 수 없는 것을 할 수 있으며, 웹팩에서 중요한 부분입니다.

    module.exports = {
      /*...*/
      plugins: [
        new HTMLWebpackPlugin()
      ]
      /*...*/
    }

HTMLWebpackPlugin 플러그인은 HTML파일은 자동적으로 생성하고 자바스크립트 번들 위치에 추가를 합니다. ([다양한 플러그인 보기](https://webpack.js.org/plugins/))

유용한 플러그인으로는 CleanWebpackPlugin가 있으며 출력을 하기 전에 dist/ 폴더를 지웁니다.

    module.exports = {
      /*...*/
      plugins: [
        new CleanWebpackPlugin(['dist']),
      ]
      /*...*/
    }

## 웹팩 모드

웹팩 4에서 소개된 모드는 각 웹팩이 동작하는 환경을 설정합니다. development 혹은 production으로 설정할 수 있으며 디폴트값은 production입니다. 그래서 development 환경이 필요할 때 설정을 하면 됩니다.

    module.exports = {
      entry: './index.js',
      mode: 'development',
      output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'app.js'
      }
    }

Development mode

- 매우 빠른 빌드
- 프로덕션보다 덜 최적화
- 코멘트를 삭제하지 않음
- 좀 더 자세한 에러 메세지와 수정 사안 제안
- 좀 더 효율적인 디버깅 환경

Production 모드는 최적화를 위해 빌드되는 데 좀 더 시간이 소요됩니다. 좀 더 작은 자바스크립트 파일이 출력되며 production에서 불필요한 내용을 제거됩니다.

샘플 앱을 만들어서 콘솔을 찍어봤습니다.

production 번들

development 번들

## 웹팩 실행시키기

글로벌로 설치했을 경우, CLI 메뉴얼대로 실행할 수 있습니다. 만약 package.json에 스크립트로 삽입되어 있다면 npm 혹은 yarn으로 실행시켜야 합니다.

아래 예시와 같이 package.json에 스크립트가 정의되어 있다면

npm run build 혹은 yarn run build(혹은 yarn build)으로 웹팩을 실행시켜야 합니다.

    "scripts": {
      "build": "webpack"
    }

## 변화 감지

웹팩은 앱 변화가 감지되면 자동으로 다시 빌드되고 다음 변화를 기다립니다

아래 스크립트를 추가하는 것만드로도 가능합니다.

그리고 npm run watch 혹은 yarn run watch(혹은 yarn watch)를 실행시켜주면 됩니다.

    "scripts": {
      "watch": "webpack --watch"
    }

watch모드의 좋은 기능 중 하나는 빌드 에러가 없을 경우에 빌드된다는 것입니다. 에러가 있다면 watch는 변화를 기다리며 다시 빌드를 시도합니다. 그리고 현재 번들에 영향을 주지 않습니다.

## 이미지 핸들링

웹팩은 file-loader 로더로 이미지를 매우 효율적으로 사용할 수 있게 해줍니다.

환경설정은 아래와 같이 간단합니다.

    module.exports = {
      /*...*/
      module: {
        rules: [
          {
            test: /\.(png|svg|jpg|gif)$/,
            use: [
              'file-loader'
            ]
          }
        ]
      }
      /*...*/
    }

자바스크립트에서 아래와 같이 이미지를 import할 수 있습니다.

    import Icon from './icon.png'

    const img = new Image()
    img.src = Icon
    element.appendChild(img)

위에 img는 HTMLLmageElement입니다. ([이미지 도큐먼트](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/Image))

file-loader는 fonts, CSV files, XML 등과 같이 다른 타입도 핸들링할 수 있습니다.

이미지와 함께 사용하기 좋은 로더는 url-loader입니다.

아래 로더 예시는 8KB 작은 PNG파일을 [data URL](https://flaviocopes.com/data-urls/)으로 로드합니다.

    module.exports = {
      /*...*/
      module: {
        rules: [
          {
            test: /\.png$/,
            use: [
              {
                loader: 'url-loader',
                options: {
                  limit: 8192
                }
              }
            ]
          }
        ]
      }
      /*...*/
    }

## SASS 코드를 CSS 파일로 변경하는 프로세스

sass-loader, css-loader, style-loader을 이용합니다.

    module.exports = {
      /*...*/
      module: {
        rules: [
          {
            test: /\.scss$/,
            use: [
              'style-loader',
              'css-loader',
              'sass-loader'
            ]
          }
        ]
      }
      /*...*/
    }

## 소스맵 생성

웹팩은 코드를 묶기 때문에 소스 파일은 오류를 일으킨 원본 파일에 대한 참조를 가져와야합니다.

devtool 속성을 사용해서 소스 맵을 생성하도록 웹팩에게 지시합니다.

    module.exports = {
      /*...*/
      devtool: 'inline-source-map',
      /*...*/
    }

devtool은 많은 값이 있으면 일반적으로 사용되는 값은 아래와 같습니다.

- none: 소스맵을 생성하지 않음
- source-map: production에서 사용하기 이상적이며, 최소화할 수 있는 별도의 소스 맵을 제공하고 번들에 참조를 추가하므로 개발 도구는 소스맵을 사용할 수 있는 것을 알고 있습니다. 디버깅 목적으로만 사용해야합니다.
- inline-source-map: development에서 사용하기 이상적으로 소스 맵을 DATA URL 인라인으로 표시합니다.
