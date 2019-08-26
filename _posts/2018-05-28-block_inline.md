---
layout: post
title: block과 line 비교
permalink: posts/blockandinline
tag: [frontend, html, css, inline, block]
---

### block

- margin collapse 현상
  - box 안의 block1에게 margin-top을 주게되면 부모로부터 margin-top이 적용되는 것이 아니라, 부모도 같이 margin-top 적용되는 것을 확인할 수 있다. 이는 margin collapse 현상이고, 이를 해결하기위해서 border 값을 적용하면 된다.

<iframe height='265' scrolling='no' title='blockNinline' src='//codepen.io/austinpark420/embed/RJbrKw/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/austinpark420/pen/RJbrKw/'>blockNinline</a> by YongMin Park (<a href='https://codepen.io/austinpark420'>@austinpark420</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### inline

- margin-top은 content flow에 영향을 줄 수 있기때문에 적용이 안된다.(margin-bottom도 동일)

<iframe height='265' scrolling='no' title='blockNinline' src='//codepen.io/austinpark420/embed/RJbrKw/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/austinpark420/pen/RJbrKw/'>blockNinline</a> by YongMin Park (<a href='https://codepen.io/austinpark420'>@austinpark420</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### block VS inline

- block의 경우 padding은 context 안쪽으로 여백이 생기고, inline의 경우 context 밖으로 여백이 생긴다.
  <iframe height='265' scrolling='no' title='blockNinline' src='//codepen.io/austinpark420/embed/RJbrKw/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/austinpark420/pen/RJbrKw/'>blockNinline</a> by YongMin Park (<a href='https://codepen.io/austinpark420'>@austinpark420</a>) on <a href='https://codepen.io'>CodePen</a>.
  </iframe>
