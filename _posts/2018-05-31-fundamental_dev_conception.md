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

- Hoisting
  * 선언문이 코드 최상위로 올라간 것처럼 작동하는 것.
  * javascript 엔진은 runtime 이전에 코드를 훑으면서 선언문에 대한 정보를 먼저 저장한다.
  * 변수 hoisting: 선언, 초기화, 할당 중 선언, 초기화 까지만 이뤄지는 것.
  * 함수 hoisting: 선언, 초기화, 할당 모두 이루어져 함수 선언 이전에 호출할 수 있는 것.
    * 함수선언식의 경우, 함수 hoisting이 일어난다.
    * 함수표현식의 경우, 함수를 값으로 변수에 저장하는 방식이기 때문에 변수 hoisiting이 일어난다.