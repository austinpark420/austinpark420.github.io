---
layout: post
title: javascript 개념정리 1
permalink: posts/javascript_concept1
tag: [javascript]
---

> 해당 포스트는 [front-end-interview-handbook](https://github.com/yangshun/front-end-interview-handbook/blob/master/Translations/Korean/questions/javascript-questions.md#%ED%94%84%EB%A1%9C%ED%86%A0%ED%83%80%EC%9E%85-%EC%83%81%EC%86%8D%EC%9D%B4-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%9E%91%EB%8F%99%ED%95%98%EB%8A%94%EC%A7%80-%EC%84%A4%EB%AA%85%ED%95%98%EC%84%B8%EC%9A%94)를 참고하여 작성하였습니다.

1 이벤트 위임(Event Delegation)

- 1.1 정의
  > 이벤트 리스너를 하위요소가 아닌 상위 요소에 추가하는 것입니다.
- 1.2 장점
  > 모든 하위요소에 이벤트를 바인딩하는 것이 아니라, 상위요소에 바인딩 하기 때문에 메모리 사용공간을 줄일 수 있습니다.

---

2 Lexical 스코프

- 2.1 정의
  > 함수를 어디서 호출했는지가 아니라, 어디서 정의를 했는지에 따라 스코프가 결정되는 것입니다.
  > javascipt의 상위 스코프를 결정할 때 Laxical 스코프 방식를 따릅니다.

---

3 This가 동작하는 방법

- 3.1 정의
  > This는 함수 호출 패턴에 따라 다르게 정의됩니다.
- 3.2 This가 정의되는 호출패턴
  1.  기본적으로 This는 전역객체에 바인딩 됩니다. ex. 전역함수, 콜백함수, 내부함수(일반함수, 메소드, 콜백함수 어디에서 선언이 되어 있던지 상관없이 전역객체에 바인딩 됩니다.)
  2.  메소드 내부의 This는 메소드가 속해있는 객체에 바인딩 됩니다.
  3.  생성자함수 안에 This는 새로 생성될 인스턴스에 바인딩 됩니다.
  4.  apply/call/bind는 바인딩할 객체를 임의적으로 선택해서 This를 바인딩 시킵니다.
