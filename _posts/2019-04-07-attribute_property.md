---
layout: post
title: attribute 와 property의 차이점은 무엇인가요?
permalink: posts/attribute-property
tag: javascript HTML
---

> 해당 포스트는 [What is the difference between properties and attributes in HTML?](https://stackoverflow.com/questions/6003819/what-is-the-difference-between-properties-and-attributes-in-html)을 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

HTML 소스코드를 작성할 때, HTML 엘리먼트안에서 attribute를 정의할 수 있습니다. 브라우져가 코드를 퍼서한 응답으로 DOM 노드가 생성됩니다. 노드는 객체이므로 그들은 property를 가지고 있습니다.

아래 HTML 엘리먼트는 2개의 attribute를 가지고 있습니다.

```html
<input type="text" value="Name:" />
```

브라우저가 위에 코드를 퍼서한 후 [HTMLInputElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement)객체가 생성되고, accept, accessKey, align, alt, attributes, autofocus, baseURI, checked, childElementCount, childNodes, children, classList, className, clientHeight 등의 property를 가지고 있습니다.

주어진 DOM 노드 객체 property를 가지고 있고, attribute는 attribute property의 구성요소입니다.

DOM 노드가 주어진 HTML 엘리먼트에 의해 생성되면
