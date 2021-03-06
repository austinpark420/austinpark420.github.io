---
layout: post
title: ES6에서 class를 어떻게 사용할까요?
permalink: posts/class
tag: [javascript]
---

> 해당 포스트는 [How to Use Classes and Sleep at Night](https://medium.com/@dan_abramov/how-to-use-classes-and-sleep-at-night-9af8de78ccb4)를 참고하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

자바스크립트 커뮤니티에서 ES6 클래스가 좋지않다는 의견이 생기고 있습니다.

- 클래스는 자바스크립트의 핵심인 프로토타입 상속을 애매하게 합니다.
- 클래스는 상속을 권장하지만 일반적으로 컴포지션을 선호합니다.
- 클래스는 첫 번째 나쁜 디자인에 사고를 가두려는 경향이 있습니다.

제(필자) 생각에는 자바스크립트 커뮤니티가 클래스의 사용과 상속의 문제점에대해서 관심을 가지는 것은 좋은 형상이라고 생각합니다. 하지만 필자는 주니어가 '클래스는 좋지않고 자바스크립트 언어에 추가되었다'고 혼돈할까봐 걱정입니다. 좀 더 혼란스러운 부분은 어떤 라이브러리들(특히 React)은 도큐먼트 전체에서 ES6 클래스를 사용합니다. React는 의도적으로 좋지않은 관습을 따르는 걸까요?

저(필자)는 클래스의 사용이 제한적이기때문에 광범위한 클래스사용이 필요악이라고 생각하는 애매한 시기에 있다고 생각합니다. 모든 프레임워크에서 사용하는 새로운 ad-hoc 클래스시스템을 학습하는 것보다 더 낫다는 믹신형태의 다중 상속 방법을 가지고 있습니다.

만약 함수형 프로그래밍을 선호한다면, 독점적인 클래스 시스템에서 "stripped down" ES6 클래스(no mixins, no autobinding, 등)로 전환함으로써 어떻게 함수형 프로그램밍으로 한걸은 더 다가갔는지 알 수 있을 겁니다.

그 동안, 클래스를 사용하는 방법이 아래 있습니다.

- 클래스를 오픈 API로 만드는 것을 거부하세요(물론 React 컴포넌트를 직접사용하지 않기때문에 내보내는 것은 예외입니다.)
  클래스를 항상 팩토리 함수뒤로 숨길 수 있습니다. 만약 클래스를 노출한다면, 사람들은 클래스로부터 전혀 이치에 맞지않게 물려받을 수 있고 나중에 깨질 수 있습니다. 사람들이 클래스를 망가뜨리는 것을 피하는 방법은 어렵습니다. 왜냐하면 그들은 메소드 이름을 당신이 미래 버전으로 사용할 수 있습니다. 그들은 당신의 프라이빗 이름으로 읽을 수 있고, 당신의 인스턴스에 그들의 상태를 부여할 수 있습니다. 그리고 supper 호출없이 당신의 메소드를 오버라이드할 수 있습니다. 운이 좋으면 그것이 작동할 수도 있지만 나중에 문제가 생길 것입니다. 그 말은 React 컴포넌트와 같이 기본적인 클래스와 유저가 만든 클래스들의 사이에 상호작용이 없으면 기본적인 클래스를 노출하는 것은 유효한 API 선택하는데 굉장히 좋은 것입니다.

- 한번 이상 상속을 받지 마세요. 상속은 편리할 수 있습니다.
  한번 상속받는 것은 나쁘지 않지만 그 이상은 하지 않는게 좋습니다. 상속과 관련된 문제는 상속을 받은 클래스가 기본적인 클래스에 너무 깊게 접근할 수 있다는 것과 그 반대의 상황입니다. 요구사항이 바꼈을 때, 클래스 계층을 리팩토링하는 것이 어려울 수 있습니다. 클래스 계층을 새롭게 만드는것 대신에 여러개의 팩토리 함수를 만드는 것을 고려해보세요. 그것은 체이닝이라고 부를 수 있습니다. 또한 기본적인 팩토리 함수를 전략객체 모듈링으로 받아드릴 수 있도록 가르칠 수 있고 제공된 다른 팩토리할수를 가질 수 있습니다. 당산의 선택과 상관없이, 중요한 부분은 모든 스텝에서 input과 output을 유지하는 것입니다. "당신은 메소드를 오버라이드할 필요가 있습니다."는 말은 명백한 API가 아니고 잘 디자인하기도 어렵습니다. 그러나 "당신이 인수로 함수를 제공할 필요가 있다."라는 망은 명백하고 그것을 통행 생각할 수 있습니다.

- 메소드에서 supper을 호출하지 마세요.
  만약 상속된 클래스에서 메소드를 재정의한다면 완벽하게 재정의하세요. 스퀀시 supper 콜을 추적하는 것은 굉장히 복잡하고 찾기 어려울 수 있습니다. 그것은 단지 다른 사람이 그런 행동을 할때 재미있을 수 있습니다. 만약 supper 메소드의 결과를 변환할 필요가 있거나 혹은 다른 일을 하기전후에 그것을 해야한다면? 이전에 포인트를 보세요. 당신의 클래스를 팩토리함수로 바꾸고 그들의 관계를 명백하게 하세요. 당신이 파라미터와 리턴 값만 가지고 있다면 의존성의 균형을 파악하기 쉽습니다. 중급 함수는 상위와 하위보다 다른 인터페이스를 가질 수 있습니다. 클래스는 메카니즘을 쉽게 제공하지 않습니다. 왜냐하면 기본적인 클래스 사용을 위한 메소드나 상속된 클래스 사용을 위한 메소드를 설계할 수 없기 때문입니다. 그러나 함수는 자연스럽게 그것을 만들 수 있습니다.

- 사람들이 당신의 클래스를 사용할거라는 기대를 하지 마세요.
  당신의 클래스를 퍼블릭 API로 제공한다면, input을 받았을때 덕타이핑을 선호하세요. instanceof checks 대신에 유저가 올바른 방법으로 사용할 것이라는 사실을 믿으세요. 이것은 iframe 및 자바스크립트 시행 컨텍스트와 관련된 문제를 제거할뿐만 아니라 사용자 층 확장 및 나중에 쉽게 조정할 수 있습니다.

- 함수형 프로그래밍을 배우세요.
  당신이 클래스안에서만 생각하지 않는 것을 도울 수 있습니다. 그래서 문제점을 알고도 사용하는 일은 없을 겁니다.

## 그래서 React 컴포넌트는 무엇인가요?

왜 이것이 끔찍한 생각인지 인지하기를 바랍니다.

```javascript
import { Component } from 'react';

class BaseButton extends Component {
  componentDidMount() {
    console.log('헤이');
  }

  render() {
    return <button>{this.getContent()}</button>
  }
}

class GreenButton extedns BaseButton {
  componentDidMount() {
    super.compoentDidMount();
    console.log('호');
  }

  getContent() {
    return '나는 초록색이야';
  }

  render() {
    <div className='green'>
      {super.render()}
    </div>
  };
}
```

그러나 저(필자)는 아래의 코드가 더 좋다고 생각합니다.

```javascript
import { component } from "react";

class Button extends Component {
  componentDidMount() {
    console.log("헤이");
  }

  render() {
    return (
      <div className={this.props.color}>
        <button>{this.props.children}</button>
      </div>
    );
  }
}

class GreenButton extends Component {
  componentDidMount() {
    console.log('호')
  }

  render() {
    return {
      <Button color="green">
        나는 초록색이야
      </Button>
    }
  }
}
```

우리는 class 키워드를 사용했지만 component를 상속받으면서 class 계층을 만들지 않았습니다. 당신이 원한다면 그것에 대한 룰을 쓸수 있습니다. 위에 코드처럼 class를 사용하는 것을 피하기위해 hoops를 사용할 필요가 없습니다.

당신이 일반적인 방법으로 추가적인 기능을 component를 공급하기를 원한다면 상위 component들은 모든 사용 사례를 다룹니다. 기술적으로 그것들은 단지 상위 함수입니다.

상위 component를 발견한 후에, 필자는 createClass() 스타일의 mixins 또는 다른 컴포지션 솔루션이 필요치 않다고 느꼈습니다. 이것은 다른 class를 사용하는 것을 선호하는 것과는 다른 문제입니다.

React 0.14에서 순수함수로 component를 쓸 수 있습니다. 이것은 정말 가치있는 일입니다. class대신 함수를 사용하는 것 또한 그렇습니다.

라이프사이클 훅이나 state가 필요할 때 아직까지 React는 순수한 기능적인 솔루션을 제공합니다. 위에 주어진 class 사용방법을 어거지 않으면 큰 이슈는 없습니다. ES6 class를 순수 기능 접근으로 마이그레이션하는 것이 더 쉬울 것입니다.

필자는 컴포지션 솔루션을 사용하는것에 대해 걱정하고 있습니다. 그 컴포지션 솔루션은 직접적으로 React 컴포지션 모델에 해를 끼치는 것이 아니고 필자의 견해로는 mixins에 가깝고 기능적인 페러다임에 말이 안됩니다.

그래서 React component를 위한 조언은 아래와 같습니다.

- 만약 2번 상속을 받지않고 super을 사용하지 않는다면 class를 사용할 수 있습니다.
- 가능하면 React component를 순수 함수로 사용해야합니다.
- 라이프사이클 훅 state가 필요하다면 component를 위해 ES6 class를 사용하세요.
- React.Component를 직접 상속을 받으세요.
- React 팀에게 직접 피드백을 주세요.
