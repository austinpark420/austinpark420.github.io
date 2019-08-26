---
layout: post
title: 함수형 자바스크립트란?
permalink: posts/functionalJavascipt
tag: [javascript, function]
---

> 해당 포스트는 [Functional Programming in JavaScript](https://codeburst.io/functional-programming-in-javascript-e57e7e28c0e5)를 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

우리는 해당 아티클에서 선언적 패턴, 순수 함수, 이뮤터빌리티와 사이드 이팩트에 대해서 학습할 예정입니다.

## 함수형 자바스크립트란 무엇인가?

- 컴퓨터사이언스에서 함수형 자바스크립트는 프로그래밍 패턴 혹은 패러다임입니다.(구조를 설계하는 스타일과 컴퓨터 프로그램 스타일)
- 함수형 프로그래밍은 매우 정확한 함수의 평가로 계산을 취급합니다.
- 함수형 프로그래밍은 상태변화와 변경 가능한 데이터를 피합니다.

위에 정의된 내용은 위키피디아에서 참조한 내용이며 지금부터 함수형 프로그래밍의 가치와 이점에대해서 살펴보겠습니다.

## 주요한 프로그래밍 패러다임과 패턴

- 절차적 프로그래밍
- 객체지향형 프로그래밍
- 메타 프로그래밍
- 명령적 프로그래밍
- 선언적 프로그래밍

절차적 프로그래밍은 절차적인 호출을 기본 컨셉으로 간단하게 계산 순서가 정해져있습니다. 주어진 절차는 어떤 상태에서든지 프로그램실행 상태에서 불려질 수 있으며 다른 절차 혹은 자체로 불릴 수 있습니다. 유명한 절차형 프로그래밍의 언어로는 COBOL, BASIC, C, ADA, GO가 있습니다.

객체지향형 프로그래밍은 객체를 기본 컨셉으로 하고 있습니다. 그 객체는 데이터와 메소드를 포함하고 있습니다. 이 패턴은 함수형 프로그래밍과 밀접한 관계가 있습니다. 주요 객체지향형 프로그래밍 언어는 C++, Java, C#, Python, Ruby, Swift 등이 있습니다.

메타 프로그래밍은 그들의 데이터를 가지고 프로그램을 다루는 능력이 있습니다. 이는 프로그램이 다른 프로그램을 읽고 생성하고 분석할 수 있게 설계되었고 심지어 실행중에 자체적으로 수정이 가능합니다.

명령적 패턴은 어떻게 프로그램이 운영되고 컴퓨터가 수행할 명령으로 구성됩니다.

선언적 패턴은 어떤 프로그램이 결과를 달성하는 방법에 초점을 두지 않고 수행하는 것 자체에 초점을 둡니다.

함수형 프로그래밍은 선언적 패턴을 따릅니다.

```javascript
var book = [
  { name: "JavaScript", page: 450 },
  { name: "Angular", page: 902 },
  { name: "Node", page: 731 }
];
// 명력형 패턴
for (var i = 0; i < book.length; i++) {
  books[i].lastRead = new Date();
}

// 선언적 패턴
book.map(book => {
  book.lastReadBy = "me";
  return book;
});

console.log(books);
```

- 위에 코드스니펫에서 book에 새로운 값을 추가했고 2가지 다른 방법으로 구현했습니다.
- 첫 번째 for loop의 접근은 배열의 길이만큼 순회하면서 배열 인덱스를 체크하고 인텍스 값을 올리고 있습니다. 그래서 이 프로그램 혹은 코드는 원하는 아웃이 어떻게 동작하는지 초점을 맞추고 있습니다.
- 두 번째 접근은 자바스크립트의 순수 메소드인 map()을 활용했고 map()은 인자로 함수를 취하고 그 함수가 각 요소를 가지고 옵니다. 이 경우에는 코드가 어떻게 동작하는지 묘사하지 않고 무엇이 실행되는지 그리고 map() 메소드는 내부적으로 실제 동작하는 것을 담당합니다.

## 매우 정확한 함수 혹은 순수 함수

수학에서 함수는 인풋과 아웃풋 사이에서 관계를 가리킵니다. 아웃풋은 각각의 인풋의 조합으로 하나의 아웃풋을 생성합니다.

함수형 프로그래밍에서 이러한 종류의 함수를 순수합수라고 칭하며 함수로부터 전달 받은 인풋데이터와 관련이 있으며 반환한 데이터를 제외하고 입력 데이터를 변경하지 않습니다.

Math.random()은 순수함수가 아닙니다. 왜냐하면 호출할 때마다 새로운 함수를 반환하기 때문입니다.

Math.min(1, 2)는 순수함수입니다. 순수함수는 항상 입력한 인풋과 같은 값을 리턴합니다.

## 왜 함수형 프로그래밍인가?

- 그것은 순수함수로 해당 스코프밖에서 값이 변하지 않습니다.
- 복잡성을 줄이고 어떻게 동작하는지 걱정할 필요가 없고 그것이 무엇을 하는지에만 집중하면 됩니다.
- 테스팅이 쉽습니다. 왜냐하면 어플리케이션 상태에 의존하지 않고 값을 확인하는 것이 쉽습니다.
- 코드를 읽기 쉽게 합니다.
- 함수형 프로그래밍은 코드를 이해하기 쉽게 만듭니다.

## 함수형 프로그래밍의 예

### 배열 함수

```javascript
let mettups = [
  { name: "JS", isActive: true, members: 450 },
  { name: "Angular", isActive: true, members: 900 },
  { name: "Node", isActive: false, members: 900 }
];

// 명령형: 프로그램이 어떻게 동자하는지 초점을 맞춤
let activeMeetups = [];
for (let i = 0; i < meetups.length; i++) {
  let m = meetups[i];
  if (m.isActive) {
    activeMeetups.push(m);
  }
}
console.log(activeMeetups); // 아웃풋은 isActive가 true인 2개의 요소입니다.

// 선언형: 무슨 프로그램이 실행되는지
let activeMeetupsFP = [];
activeMeetupsFP = meetups.filter(m => {
  return m.isActive;
});
console.log(activeMeetupsFP); // 아웃풋은 isActive가 true인 2개의 요소입니다.
```

위에 예에서 우리는 active인 meet-ups를 필터이 했고 2가지 다른 방법으로 접근했습니다. 두 번째 접근은 함수형 프로그래밍으로 filter() 메소드안에 '어떻게 동작하는지'에 대한 내용이 담겨있고 프로그램은 오직 meetups 배열같은 인풋과 activeMeetupsFP 아웃풋에 초점을 맞추고 있습니다. 반면 첫 번째 접근은 for문을 통해서 프로그램이 어떻게 동작하는지에 관심을 가지고 있습니다.

간단하게 아래의 여러 메소드들은 함수형 프로그래밍을 하는데 도움을 주고 코드의 복잡성을 감소시킵니다.

- find
- map
- reduce
- every
- some

[깃허브 레포](https://github.com/npatro/functional-programming/tree/master/code)에서 위에 메소드의 사용법을 참고하세요.

## 함수 체이닝

이것은 여러 메소드를 실행하기위한 메카니즘입니다. 각 메소드는 객체를 리턴하고 호출문이 구문과 함께 중간에 변수를 저장할 변수를 요청하지 않고 체이닝되도록합니다.

```javascript
let mettups = [
  { name: "JS", isActive: true, members: 450 },
  { name: "Angular", isActive: true, members: 900 },
  { name: "Node", isActive: false, members: 600 },
  { name: "React", isActive: false, members: 500 }
];
let sumFPChain = meetups
  .filter(m => {
    return m.isActive;
  })
  .map(m => {
    return m.members - 0.1 * m.members;
  })
  .reduce((acc, m) => {
    return acc + m;
  }, 0);
console.log(sumFPChanin); // 아웃풋은 1890
```

위에 코드 스니펫에서 10% 멥버가 중복이라는 가정하에 활성 밋업 멥버의 총합을 프린트하고 싶습니다.

## 함수형 프로그래밍을 서포트하는 라이브러리

코드를 좀 더 선언적으로 맏르어주는 라이브러리

- RamdaJS
- UnderscoreJS
- lodash

## 사이드 효과

함수 혹은 표현식은 프로그램의 상태를 변경하면 사이드 효과가 나타날 수 있습니다.

```javascript
let meetup = { name: "JS", isActive: true, members: 49 };

const scheduleMeetup = (date, place) => {
  metup.date = date;
  metup.place = place;

  if (meetup.members < 50) meetup.isActive = true;
};

const publishMeetup = () => {
  if (meetup.isActive) {
    meetupt.publish = true;
  }
};

schduleMeetup("today", "Bnagalore");
publishMeetup();
console.log(meetup);
```

프로그램에 사이드 효과가 있습니다. 왜냐하면 실제 scheduleMeetup 함수는 date와 place를 meetup에 추가합니다. 그리고 isActive를 수정합니다. 또한 publishMeetup은 인풋이 변경되었기 때문에 사이드 효과가 나타납니다. 큰 프로그램에서는 디버깅을 하는 것이 정말 어렵습니다.

사이드 효과가 항상 나쁜 것은 아니지만 언제 그런 상황이 발생할지 조심해야합니다.

## 불변성

불변성은 하나의 함수가 원래 값을 변경하지않고 새로운 복사본을 만드는 것에 중요한 역할을 합니다.

배열과 객체가 여러 함수를 통과하고 불변성을 유지할 수 없다면 배열과 객체의 복사본을 만들 수 없을 겁니다.

이것은 여러 객체와 배열에서 디버깅하기 정말 어렵게 만듭니다.

변경 가능한 것이 항상 나쁜 것은 아니지만 조심해야 합니다.

## 불변성 라이브러리

자바스크립트는 기본적으로 배열과 객체가 변하지 않도록 기능을 제공하지 않습니다. 불변성을 가지는데 도움을 주는 라이브러리는 아래와 같습니다.

- Seamless-immutable
- Immutable JS

## 요약

함수형 프로그래밍은 순수하고 작은 함수의 집합이며 불변성을 가지고 사이드 효과가 작습니다.
