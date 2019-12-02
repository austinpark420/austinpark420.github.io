---
layout: post
title: jquery의 on.(handler, fn) 와 handler.(fn) 의 차이점
permalink: posts/jqueryHandler
tag: project
---

> 해당 포스트는 [Difference between .on('click') vs .click()](https://stackoverflow.com/questions/9122078/difference-between-onclick-vs-click)를 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

두 가지의 차이점은 사용 패턴에 있고 on.(handler, fn)을 사용하는 것을 추천드립니다.

아래 html 코드에 새로운 버튼을 추가한다고 가정해 봅시다.

```html
<html>
  <button id="add">Add new</button>
  <div id="container">
    <button class="alert">alert!</button>
  </div>
</html>
```

```javascript
$('button#add').click(function() {
  var html = "<button class='alert'>Alert!</button>";
  $('button.alert:last')
    .parent()
    .append(html);
});
```

그리고 "Aler!"라는 경고를 보여주기 위해서 우리는 "click" 와 "on" 둘다 사용할 수 있습니다.

---

### Click을 사용할 때

```javascript
$('button.alert').click(function() {
  alert(1);
});
```

선택자와 일치하는 모든 단일 요소에 대해서 핸들러가 생성됩니다.

1. 일치하는 요소가 많으면 동일한 핸들러가 생성되고 메모리의 사용량을 증가시킵니다.
2. 동적으로 추가된 요소에는 핸들러를 가질 수 없습니다. 즉 동적으로 추가된 "Alert!"에 핸드러를 리바인드해주지 않으면 버튼이 동작하지 않습니다.

### .on 을 사용할 때

```javascript
$('div#container').on('click', 'button.alert', function() {
  alert(1);
});
```

위에 코드를 보시면 하나의 핸들러가 매치되는 모든 요소에 대한 하나의 핸들러가 동작하며, 동적으로 추가된 요소 또한 포함합니다.
