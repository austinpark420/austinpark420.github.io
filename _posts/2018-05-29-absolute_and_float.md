---
layout: post
title: absolute와 float 비교
permalink: posts/absoluteandfloat
tag: frontend html css absolute float
---

absolute와 float는 모두 일반적인 흐름을 벗어난다. 그렇다면 그 이외에 어떤 차이가 있는지 알아보자.

### absolute

- 레이어이기 때문에 absolute 위에 absolute가 겹칠 수가 있다.
- 논리적인 흐름상에 있는 line 속성 위에 떠 있을 때 line 속성을 가린다.

<iframe height='265' scrolling='no' title='absolute' src='//codepen.io/austinpark420/embed/BVBbXB/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/austinpark420/pen/BVBbXB/'>absolute</a> by YongMin Park (<a href='https://codepen.io/austinpark420'>@austinpark420</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### float

- 보모 크기만큼의 line box가 생기면서 논리적인 흐름을 벗어나고, 레이어가 아니기때문에 absolute처럼 겹치지 않는다.
- 논리적인 흐름상에 있는 line 속성 위에 떠 있을 때 line 속성을 밀어낸다.

<iframe height='265' scrolling='no' title='flaot' src='//codepen.io/austinpark420/embed/bKbZOb/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/austinpark420/pen/bKbZOb/'>flaot</a> by YongMin Park (<a href='https://codepen.io/austinpark420'>@austinpark420</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
