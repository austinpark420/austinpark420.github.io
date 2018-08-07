---
layout: post
title: Angular Study
permalink: posts/angular_study
tag: frontend Angular
---

### Angular CSS
  * :host
    * 컴포넌트 자기 자신을 가리킨다.
    * CBD 개발 방식에서 CSS를 적용하기 위해 필요한 방법이다.

### ngModule
  * 관련있는 구성요소를 하나의 단위로 묶는 메커니즘을 말한다.
  * Angular는 하나 이상의 모듈을 가져야 한다.
  * 다른 모듈을 import할 수 있다.
  * 코드가 복잡해지면 크게 루트, 공유, 기능, 핵심모듈로 어플리케이션을 구성하는 것이 좋다.

### 라이브러리 모듈
  * Angular에서 제공하는 빌트인 모듈이다.

### 서비스
  * 컴포넌트에서 뷰를 구성하는 구성요소를 제외해 하나의 기능으로 묶은 것.

### 싱글턴
  * 생성자가 여러 차례 호출된다고 하더라도 실제로 생성되는 객체는 하나이다.

### 의존성 주입
  * 구성요소를 느슨한 관계가 될 수 있도록 의존 관계를 코드 외부에서 정의를 하는 것.
  * Angular에서는 프레임워크 자체에서 의존성 주입을 지원한다.

### 서비스 중재자 패턴
  * 컴포넌트 간의 불필요한 데이터 공유를 줄이고, 일정한 자료구조로 데이터를 공유할 수 있는 것.

### 라우트 순서
  1. URL path 와 component가 쌍으로 이루어진 라우트 생성
  2. RouterModule.forRoot 또는 RouterModule.forChild를 호출하여 라우트 구성이 포함된 모듈을 생성
  3. <router-oulet>으로 뷰가 렌더링될 위치 지정
  4. routerLink 프로퍼티로 네이게이션 작성