---
layout: post
title: 네이티브객체와 호스트객체는 무엇이 다를까요?
permalink: posts/hostObj_vs_nativeObj
tag: [javascript, object]
---

> 해당 포스트는 [What is the difference between native objects and host objects?](https://stackoverflow.com/questions/7614317/what-is-the-difference-between-native-objects-and-host-objects)를 참고하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

아래 내용은 ECMAScript에 게제되어있는 스펙입니다.

### 네이티브 객체

- 네이티브객체는 호스트 환경 아니라 ECMAScript의 스펙에 의해서 정의된 객체입니다.
  NOTE 표준 네이티브객체는 위에 언급한 스펙으로 정의되어 있습니다. 약간의 네이티브객체들은 빌트인이고 나머지는 ECMAScipt 프로그램이 실행되는 동안 구성됩니다.

  예시: Object (constructor), Date, Math, parseInt, eval, string methods like indexOf and replace, array methods, ...

참조: [http://es5.github.com/#x4.3.6](http://es5.github.com/#x4.3.6)

### 호스트 객체

- ECMASrcipt의 실행 환경을 만들기위해 호스트 환경에서 제공된 객채입니다.
  NOTE 네이티브객체가 아니면 호스트객체 입니다.

  예시(브라우저 환경일 때): window, document, location, history, XMLHttpRequest, setTimeout, getElementsByTagName, querySelectorAll, ...

  참조: [http://es5.github.com/#x4.3.8](http://es5.github.com/#x4.3.8)

---
