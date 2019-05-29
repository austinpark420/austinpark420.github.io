---
layout: post
title: map와 forEach의 차이점
permalink: posts/mapVSforeach
tag: javascript
---

> 해당 포스트는 [JavaScript — Map vs. ForEach](https://codeburst.io/javascript-map-vs-foreach-f38111822c0f)를 참고하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

> 자바스크립트를 좀 더 깊게 배우고 싶다면? [JavaScript — Understanding the Weird Parts](https://codeburst.io/javascript-understanding-the-weird-parts-d1d0e7061ebf)

- 만약 자바스크립트를 사용한지 얼마되지 않았다면, 비슷한 2개의 자바스크립트 메소드를 보았을겁니다: Array.prototype.map()과 Array.prototype.forEach().

### 무엇이 다를까요?

## Map & ForEach 정의

우선 MDN의 정의를 살펴봅시다.

- forEach(): Array 요소를 제공된 함수로 한 번 실행합니다.
- map(): 모든 Array 요소가 제공된 함수로 호출될때 새로운 array를 생성합니다.

위에 정의는 정확히 무슨 의미일까요?

forEach() 메소드는 아무것도 리턴하지 않습니다(undefined). 단지 제공된 함수로 Array 요소를 호출합니다. 이 콜백은 호출하는 Array를 변경할 수 있습니다.

한편, map() 메소드는 Array안에 요소들을 호출합니다. forEach()와 다른점은 값을 사용하고 Array와 동일한 사이즈의 새로운 Array을 반환합니다.

### 예시

아래의 Array에서 만약 각 요소를 2배로 올리고 싶다면 map과 forEach 모두 사용할 수 있습니다.

```javascript
let arr = [1, 2, 3, 4, 5];
```

_forEach:_
forEach 메소드 안에서 아무것도 반환하지 않고 리턴 값은 버려집니다.

```javascript
arr.forEach((num, index) => {
  return (arr[index] = num * 2);
});

// 결과
// arr = [2, 4, 6, 8, 10]
```

_Map:_

```javascript
let double = arr.map(num => {
  return num * 2;
});

// 결과
// doubled = [2, 4, 6, 8, 10]
```

## 속도 측정

[JsPerf는 javascirpt 메소드와 함수 속도차이를 측정하는 좋은 사이트입니다.](https://jsperf.com/)

forEach() 와 Map()을 테스트한 결과가 아래 이미지 입니다.

![forEach() 와 Map()을 테스트한 결과](https://cdn-images-1.medium.com/max/1600/1*aVOlJ0l02ymgVrQ8axIBrQ.png)

보시다시피, 필자 컴퓨터에서 forEach()가 map()보다 70%가 속도가 느립니다. 여러분의 브라우저에서 약간 다를수도 있습니다.

[Map vs ForEach jsPerf](https://jsperf.com/map-vs-foreach-speed-test)

## 기능 측정

함수형프로그램을 선호한다면 map()을 사용하는 것이 더 바람직하다는 것을 이해하는 것이 중요합니다.

forEach() 기존의 Ararry를 변경하기 때문입니다. 반면, map()은 새로운 Ararry를 반환합니다.그러므로 기존의 배열을 변경하지 않습니다.

## 무엇이 더 좋을까요?

그것은 상황에 따라 달라집니다.

forEach()는 당신의 Array안에 데이터를 변경하려는 것이 아니라 데이터베이스에 저장하거나 로그아웃하는 것과 같은 작업에 유용할 수 있습니다.

```javascript
let arr = ["a", "b", "c", "d"];

arr.forEach(letter => {
  console.log(letter);
});

// a
// b
// c
// d
```

map()은 데이터를 변경하거할 때 선호될 수 있습니다. 더 빠를 뿐 아니라 새로운 배열을 반환합니다. 이는 다른 메소들과 함께 사용하는 것 같이 멋진 일을 할 수 있다는 것을 의미합니다.(map(), filter(), reduce() 등)

```javascript
let arr = [1, 2, 3, 4, 5];
let arr2 = arr.map(num => num * 2).filter(num => num > 5);

// arr2 = [6, 8, 10]
```

위에 우리가 했던 일들은 처음에 arr을 맵핑을하고 모든 요소를 곱하는 것입니다. 이 후 우리는 array를 통해 필터링을 하고 5보다 큰 요소만 저장했습니다. 이것은 arr2 = [6, 8, 10]으로 만들었습니다.

만약 map, reduce, filter에 대해서 더 알고 싶다. 해당 article을 참고 부탁드립니다:[JavaScript — Learn to Chain Map, Filter, and Reduce.](https://codeburst.io/javascript-learn-to-chain-map-filter-and-reduce-acd2d0562cd4)

## key point

- forEach()으로 할 수 있는 것은 map()으로도 가능하고 그 반대도 가능합니다.
- map()은 메모리를 할당하고 리턴 값을 저장합니다. forEach()는 리턴 값을 버리고 항상 undefined를 리턴합니다.
- forEach()는 콜백함수로 현재 Array를 변환할 수 있습니다. 대신에 map()은 새로운 Array를 리턴합니다.
