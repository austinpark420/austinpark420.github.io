---
layout: post
title: attribute 와 property의 차이점은 무엇인가요?
permalink: posts/attribute-property
tag: [javascript, HTML]
---

> 해당 포스트는 [What is the difference between properties and attributes in HTML?](https://stackoverflow.com/questions/6003819/what-is-the-difference-between-properties-and-attributes-in-html)을 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

HTML 소스코드를 작성할 때, HTML 엘리먼트안에서 attribute를 정의할 수 있습니다. 브라우져가 코드를 퍼서한 응답으로 DOM 노드가 생성됩니다. 노드는 객체이므로 그들은 property를 가지고 있습니다.

아래 HTML 엘리먼트는 2개의 attribute를 가지고 있습니다.

```html
<input type="text" value="Name:" />
```

브라우저가 위에 코드를 퍼서한 후 [HTMLInputElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement)객체가 생성되고, accept, accessKey, align, alt, attributes, autofocus, baseURI, checked, childElementCount, childNodes, children, classList, className, clientHeight 등의 property를 가지고 있습니다.

주어진 DOM 노드 객체 property를 가지고 있고, attribute는 attribute property의 구성요소입니다.

DOM 노드가 주어진 HTML 엘리먼트에 의해 생성되면 많은 property들은 attribute 이름과 동일하거나 비슷합니다. 하지만 1:1로 매칭되는 것은 아닙니다. 예를들어 아래 HTML 코드를 보면

```html
<input id="the-input" type="text" value="Name:" />
```

DOM 노드는 id, type, value property 및 다른 property를 가지고 있습니다.

- id property는 id attribute가 반영된 것입니다. property가 attribute값을 읽으면서 property 값을 attribute의 값으로 세팅합니다. id는 순수한 property이며 그것은 수정되거나 제한되지 않았습니다.

- type property는 type는 attribute가 반영된 것입니다. property가 attribute값을 읽으면서 property 값을 attribute의 값으로 세팅합니다. type는 순수한 property가 아닙니다. 왜냐하면 값이 제한되어 있기 때문입니다.type는 input 엘리먼트 안에서만 사용 가능합니다. 만약 `<input type="foo">`라면 theInput.getAttribute("type") "foo"를 반환하지만 theInput.type는 "text"를 반환합니다.

- 반대로 value property는 value값을 반영하지 않습니다. 대신에 input의 현재 값입니다. 사용자가 input 박스에 값을 변경하면 value property는 변경된 값을 반영합니다. input 박스에 "John"이라고 입력을 하면 리턴값을 아래와 같습니다.

```javascript
theInput.value; // return "John"
```

반면에

```javascript
theInput.getAttribute("value"); // return "Name:"
```

value property는 input 박스안에 있는 컨텐츠를 반영하지만 value attribute는 HTML 소스코드에 있는 value의 초기값을 나타냅니다.

만약에 텍스트 박스에 어떤 값이 있는지 알고 싶다면 property를 읽고, 텍스트박스에 초기값을 알고 싶다면 attribute 값을 읽으면 됩니다. 혹은 `defaultValue` property를 사용할 수 있습니다. 이것은 순수 value attribute값을 반영합니다.

```javascript
theInput.value; // return "John"
theInput.getAttribute("value"); // return "Name:"
theInput.defaultValue; // return "Name:"
```

attribute를 직접 반영하는 많은 property들이 있습니다. 일부는 약간 다른 이름으로 반영되고(예를 들어 htmlFor은 for attribute를 반영하고, className은 class attribute를 반영합니다.) 대부분은 그들의 attribute를 반영하지만 제한되거나 수정되는 부분 있습니다. 좀 더 자세한 스펙을 알고 싶으시면 [링크](https://www.w3.org/TR/html5/infrastructure.html#reflect)를 참조 부탁드립니다.
