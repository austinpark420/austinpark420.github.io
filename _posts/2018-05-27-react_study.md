---
layout: post
title: React Study
permalink: posts/react_study
tag: frontend react
---

## React

### 서버사이드 렌더링 지원
* 초기 구동 딜레이 문제점 해결.
* 검색엔진 최적화 (구글은 문제가 없지만 다른 검색엔진에서는 문제가 생길 수 있음)

### view only
* view만 담당하기 때문에 다른 기능을 추가하기 위해서는 3rd party tool이 필요하다.

### JSX
* XML-like syntax를 native javascript로 변환해주는 것.

### props
* 컴포넌트 내부에 변하지 않는 데이터.

* 기본값 설정

```javascript
class App extends React.Component {
    render() {
        return (
            <div>{this.props.value}</div>
        );
    }
};

App.defaultProps = {
    value: 0
};
```

* Type 검증

```javascript
class App extends React.Component {
    render() {
        return (
            <div>
                 {this.props.value}
                 {this.props.secondValue}
                 {this.props.thirdValue}
            </div>
        );
    }
};

App.propTypes = {
    value: React.PropTypes.string,
    secondValue: React.PropType.number,
    thirdValue: React.PropTypes.any.isRequired
};
```

* propTypes를 지정하는 것은 필수가 아니고 유지보수를 위해서 사용하는 것이다.

### state
* 컴포넌트에서 유동적인 데이터.
* 초기값 필수, 컴포넌트 생성자 method인 constructor에서 하면 된다.

### map
* map을 활용해 props와 state 연습

<iframe height='265' scrolling='no' title='how to ' src='//codepen.io/austinpark420/embed/YLmOZz/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/austinpark420/pen/YLmOZz/'>how to </a> by YongMin Park (<a href='https://codepen.io/austinpark420'>@austinpark420</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


## redux
    * 상태관리를 통합적으로 해주는 library.

### Provider
    * 하위 컴포넌트에 redux의 store에 연결해주는 역핡.

### connect([...options])
    * 컴포넌트를 redux에 연결하는 함수를 반환한다.

## immutable.js
    * JavaScript에서 배열과 객체는 pass by reference이다.
    * 직접적으로 수정한다면, 내부의 값이 수정됐을지라도 레퍼런스가 가르키는곳은 같기 때문에 똑같은 값으로 인식한다.
    * React에서 이를 상태변화로 간주할 수가 없다.
    * 그래서 새 배열이나 객체에 복사를 하는데 이를 편하게 할 수 있게 도와주는 것이 immutable.js이다.












### refer to
* [React & Express 를 이용한 웹 어플리케이션 개발하기(inflearn)](https://www.inflearn.com/course/react-%EA%B0%95%EC%A2%8C-velopert/)
