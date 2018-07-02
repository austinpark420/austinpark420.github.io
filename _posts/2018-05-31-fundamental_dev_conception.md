---
layout: post
title: 기본적인 개발용어 정리
permalink: posts/fundamentaldevconception
tag: frontend dev javascript fundemental
---

개발을 처음 시작했을 때, 많은 것들이 어려웠다. 그 중 하나가 개발용어였다. 분명 우리나라 말인데 용어의 뜻을 모르기 때문에 무슨말을 하는지 전혀 알아들을 수가 없었다. 그래서 공부하면서 나만의 언어로 정리해보기로 했다.

- Programing
  * 명령어들의 집합.

- ES5, ES6
  * ECMAScript 줄임 말, javascript 사용하는 문법.

- statement (구문)
  * 명령어의 최소 단위.

- expression (표현식)
  * 하나의 값으로 수렴하는 하는 것.

- Framework VS Library
  ![Framework vs libary](https://www.programcreek.com/wp-content/uploads/2011/09/framework-vs-library.png)

  * Framework
    * 틀
    * Framework가 제공하는 기능을 기반으로 원하는 application을 만들 수 있다.
    * Framework 룰을 따라 코드를 작성해야한다.

  * library
    * 필요할 때마다 import해서 사용하는 것.

- Control flow
  * 위에서 아래로 순차적으로 실행되는 코드를 조건문이나 반복문을 통해 실행순서를 제어하는 것이다.


- Code block (Block statement)
  * 명령어를 중괄호로 묶어놓은 것.

- Pass-by-value VS Pass-by-reference
  * Pass-by-value: immutable, 메모리에 저장된 값 자체를 참조하는 것.
  * Pass-by-reference: mutable, 메모리에 주소 값을 참조하는 것.

- Object의 property VS method
  * property: 데이터를 값으로 가지는 object key(혹은 name)
  * method: 함수를 값으로 가지는 object key(혹은 name)

- Hoisting (javascript)
  * 선언문이 코드 최상위로 올라간 것처럼 작동하는 것.
  * javascript 엔진은 runtime 이전에 코드를 훑으면서 선언문에 대한 정보를 먼저 저장한다.
  * 변수 hoisting: 선언, 초기화, 할당 중 선언, 초기화 까지만 이뤄지는 것.
  * 함수 hoisting: 선언, 초기화, 할당 모두 이루어져 함수 선언 이전에 호출할 수 있는 것.
    * 함수선언식의 경우, 함수 hoisting이 일어난다.
    * 함수표현식의 경우, 함수를 값으로 변수에 저장하는 방식이기 때문에 변수 hoisting이 일어난다.

- First-class-object
  * 하기의 조건을 충족할 때 일급객체라고 한다.
    * 무명 리터럴로 표현이 가능하다.
    * 변수나 자료구조에 저장이 가능하다.
    * 함수의 매개변수로 전달할 수 있다.
    * return 값으로 반환할 수 있다.

- 동기식(synchronous) VS 비동기(asynchronous)
  * 동기식: 실행되고 있는 task가 끝나야 다른 task를 실행할 수 있는 것.

  * 비동기식: task가 실행되고 있어도 다른 task를 실행할 수 있는 것.

- callback function
  * 함수의 매개변수에 있는 함수를 콜백함수라고 한다.
  * 주로 비동기로 동작해야할 기능이 있을 때 사용한다.

- Call-by-value VS Call-by-reference
  * Call-by-value: parameter로 전달되는 argument가 기본자료형일 때, pass-by-value와 같이 동작하는 것.
  * Call-by-reference: parameter로 전달되는 argument가 객체형일 때, pass-by-reference와 같이 동작하는 것.

- prototype 객체
  * 모든 객체의 부모역할을 하는 객체로써, javascritp에서 상속을 가능하게해주는 개념이다.

- Navtive object VS Host object
  * Navtive object
    * ECMAScript의 스펙에서 제공하는 object.
    * javascript의 runtime 환경과 상관없이 사용할 수 있는 객체.
  * Host object
    * brower 혹은 node.js와 같이 javascript의 runtime 환경에서 제공하는 객체.

- Static Method VS Prototype Method
  * Static Method: 생성자함수가 가지는 method.
  * Prototype Method: Prototype이 가지는 method, 인스턴스가 상속받아서 사용할 수 있는 Method.

- 가변인자함수
  * parameter의 갯수가 정해지지 않고 여러개의 argument를 parameter으로 전달받을 수 있는 함수.

- lexical scope
  * 함수가 선언된 시점의 scope를 가지는 것.

- Execution Context
  * 실행가능한 코드가 실행되기 위해 필요한 환경

- closer
  * ES5 조건
    1. 외부함수, 내부함수가 있어야 함.
    2. 내부함수에서 외부함수의 변수를 참조해야 함.
    3. 내부함수가 외부함수보다 라이프사이클이 길어야 한다.
  * 내부함수가 외부함수를 변수를 참조하고 있을 때, 외부함수의 라이프사이클이 종료되어서 외부함수 변수 값을 참조 할 수 있는 현상.

- DOM
  * 브라우저가 HTML을 파싱해서 해석할 수 있게 컴파일한 것.

- backend as a service[BaaS]
  * 클라우드 컴퓨팅 서비스 모델.
  * 웹 어플리케이션 혹은 앱을 백엔드 클라우드 서버에 연결해주는 기능을 하고, SDK와 API를 활용해 푸시 알람 혹은 소셜 네트워크 서비스 등을 제공한다.

- query string vs payload
  * query string: 데이터를 url창으로 보내는 것. GET 방식
  * payload: request body에 담긴 데이터. POST 방식

- 함수형 프로그래밍 vs 명령형 프로그래밍
  * 함수형 프로그래밍: 입력값으로부터 목적값을 생성하는 것.
  * 명령형 프로그래밍: 데이터의 상태를 순차적으로 변형시키는 것.

- Ajax
  * 자바스크립트를 이용해 비동기식으로 서버와 브러우저 간의 데이터를 주고 받는 통신방식을 말한다.

- REST API
  * HTTP 통신프로토콜을 효율적으로 활용하는 이론을 말한다.
  * uri에는 정보의 자원(명사)을 표현하고, HTTP Method로 자원에 대한 행위(동사)로 표현한다.

- Var vs Let vs Const
  * Var: Var 키워드로 선언한 변수는 function scope를 가진다.
  * Let: Let 키워드로 선언한 변수는 codeblock scope를 가진다. (재할당 가능)
  * Const: Const 키워드로 선언한 변수는 codeblock scope를 가진다. (재할당 불가능)
  * Let 과 Const도 Var와 마찬가지로 호이스팅이 발생하지만 Var와 다르게 일시적 사각지대가 있어 선언 전에 변수 참조가 안된다.

- Class
  * ES6에 도입된 키워드로 prototype 기반 언어를 Class기반 언어처럼 사용할 수 있게 해주는 문법적 설탕.

- promise
  * 비동기식으로 서버와 통신하는 방법 중 하나로 Ajax의 콜백헬과 에러처리 문제를 보안한 방법이다.

- Module
  * 재사용이 가능한 코드모음

- webpack
  * Module bundler

- babel
  * Transfiler