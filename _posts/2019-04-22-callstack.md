---
layout: post
title: 자바스크립트의 콜스택이란?
permalink: posts/callstack
tag: [javascript, callstack]
---

> 해당 포스트는 [Understanding the JavaScript call stack](https://medium.freecodecamp.org/understanding-the-javascript-call-stack-861e41ae61d4)를 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

브라우저와 같이 호스팅 환경에 있는 자바스크립트 엔진은 힙과 콜 스택을 포함하는 싱글스레드 인터프리터입니다. 브라우저는 DOM, AJAX, Timer와 같은 웹 API를 제공합니다.

이번 아티클에서는 콜스텍의 정의와 필요성에 대해서 이야기하려고 합니다. 콜스텍을 이해한다면 자바스크립트 엔진에서 "함수의 상속과 실행 순서" 어떻게 동작하는지 명확하게 알 수 있습니다.

콜스텍은 주로 함수가 실행(콜)되었을 때 사용됩니다. 콜스텍은 싱글이기 때문에 함수가 실행되고 종료되고가 순차적으로 발생하면 위에서부터 아래로 진행됩니다. 그렇기때문에 콜스텍은 동기식입니다.

콜스텍을 이해한다는 것은 비동기식 프로그래밍에 필수적입니다.

비동기식 자바스크립트 예시로는 콜백함수, 이벤트 루프, 테스크 큐가 있습니다. 콜백함수는 이벤트 루프에 의해 콜백함수가 스텍에 푸시된 후에 콜스텍이 실행된 상태에서 동작합니다.

본격적으로 시작하기 전에 앞서 콜스텍이 무엇인지 정의를 합시다.

기본적인 단계에서 콜스텍은 Last In First Out 일시적으로 데이터를 저장하고 함수 실행(콜)을 관리하는 데이터 구조입니다.

조금 더 자세하게 알아봅시다.

LIFO: 콜스텍을 후입선출이라는 데이터구조 동작한다고 말할 때 마지막으로 스택으로 푸시된 함수가 리턴될 때 가장 먼저 나온다는 의미입니다.

아래 후입선출을 'stack trace error'을 콘솔하면서 증명하는 코드 샘플 같이 봅시다.

```javascript
function firstFunction() {
  throw new Error("Stack Tracn Error");
}

function secondFunction() {
  firstFunction();
}

function thirdFunction() {
  secondFunction();
}

thirdFunction();
```

코드가 리턴되었을 떼 우리는 에러를 얻었습니다. 스텍이 프린트되면서 어떤 함수가 스텍에서 가징 위에있는지 알 수 있습니다.

![Stack trace error](https://cdn-images-1.medium.com/max/800/1*LIuELJ2RTtwWExRWGdu_Hw.png)

함수의 배열이 마지막으로 스텍에 들어깟던 firstFunction()이 리턴되었고, 그 다름으로는 secondFunction()이고 처음으로 스텍으로 푸시된 thirdFunction()으로 끝나는 것을 확인할 수 있습니다.

일시적인 저장: 함수가 실행(콜)되었을 때 함수, 파라미터, 변수는 스텍프레임을 형성하기위새 콜스텍안으로 푸시됩니다. 이 스텍 프레임은 스텍안에 있는 메모리 공간입니다. 함수가 리턴되었을때 메모리는 깨끗해집니다.

![LIFO](https://cdn-images-1.medium.com/max/800/1*PPkrowy4n_Pyehb_NdhLrg.png)
저작권: CMU

함수 실행(콜) 관리: 콜스텍은 각 스텍프레임의 레코드 포지션을 유지합니다. 이것은 다음에 실행될 함수를 알고 있고 실행 후에 제거를 한다는 의미입니다. 이것은 동기 자바스크립트에서 무엇이 실해되는지를 뜻합니다.

## 콜스텍은 함수 콜을 어떻게 핸들링할까요?

이에 대한 답을 간단한 코드예제를 살펴보면서 확인해 봅시다.

```javascript
function firstFunction() {
  console.log("Hello from firstFunction");
}

function secondFunction() {
  firstFunction();
  console.log("The End from secondFunction");
}

secondFunction();
```

![Here is the output](https://cdn-images-1.medium.com/max/800/1*9iSkoJoXM0Ok8iQ5mOHl5Q.png)

코드가 실행되었을 때 발생하는 일들입니다.

1. secondFunction()이 실행되었을 때, 빈 스텍 프레임이 생성됩니다. 이것은 주요한 메일 엔트리포인트입니다.
2. secondFunction()이 firstFunction()을 호출하고 그것은 스텍안으로 푸시됩니다.
3. firstFunction()은 'hello from firstFunction'을 콘솔로 프린트합니다.
4. firtsFunction()은 스텍에서 사라집니다.
5. 실행 순서는 secondFunction()으로 이동합니다.
6. secondFunction()은 'The end from secondFunction'을 콘솔로 프린트합니다.
7. secondFunction()은 스텍에서 사라지고 메모리는 깨끗해집니다.

## 스텍 오브 플로우의 원인은 무엇인가요?

스텍 오브 플로우는 끝이 없는 재귀함수때문에 발생됩니다. 브라우저는 스텍콜을 감당할 수 있는 최대치가 있습니다.

아래 코드가 예시 코드입니다.

```javascript
function callMyself() {
  callMyself();
}
callMyself();
```

callMyself()는 'Maximum call size exceeded'가 반환될때까지 실행되고 스텍 오브 플로우 현상이 발생합니다.
![Maximum call stack error](https://cdn-images-1.medium.com/max/800/1*JFRlgLp2uvbdVrh7WdmMrQ.png)

## 정리

콜스텍에서 중요한 부분은 아래와 같습니다.

1. 싱글 스레드입니다. 이것은 한 번에 한 가지일만 처리할 수 있다는 의미입니다.
2. 코드 실행은 동기식으로 진행됩니다.
3. 함수가 실행되면 일시적으로 메모리를 차지하는 스텍프레임이 형성됩니다.
4. 후입선출 방식으로 동작합니다.
