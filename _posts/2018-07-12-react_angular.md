---
layout: post
title: react 와 angular
permalink: posts/react_angular
tag: frontend dev javascript react angular
---

1. view를 그리기
  * react: class component render 메소드가 html을 그리고, css는 보통 import 한다.
  * angular: component 데코레이터의 template, styles property를 사용한다.

2. CSS framework(library) import하는 방법
  * react: framework(library)가 필요한 컴포넌트에서 import해서 사용한다.
  * angular: angular-cli.json 파일에서 통합 관리한다.

3. 컴포넌트간의 상태 공유
  * react: props로 컴포넌트간에 상태 공유를 한다.
  * angular
    * 부모가 자식에게 상태를 전달할 때 property binding을 사용한다.
      * 부모 template에 상태가 필요한 자식 component tag에 property binding으로 상태의 참조를 준다.
      * 상태를 전달받는 자식 component class에서 `@input()`으로 받는다.
    * 자식이 부모에게 상태를 전달할 때 event binding을 사용한다.

4. filter 사용법
  * react: render 함수 내부에 filter 메소드를 사용한다.
  * angular: pipe를 사용한다.

5. class attribute 동적 할당
  * react: className과 javascript으로 인터렉션을 한다.
  * angular: class(단항 vs 다항), ngClass 디렉티브로 조작한다.

