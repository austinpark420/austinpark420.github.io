---
layout: post
title: memoization이란?
permalink: posts/memoization
tag: model
---

> 해당 포스트는 [Understanding Memoization in javascript](https://scotch.io/tutorials/understanding-memoization-in-javascript)의 일부를 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

## memoization이란?

memoization은 많은 함수들의 결과를 저장하고 동일한 인풋에 캐시된 결과값을 리턴함으로써 어플리케이션의 속도를 향상시키는 최적의 기술이라고 할 수 있습니다.

## 케이스 스터디: 피보나치 수열

피보나치 수열은 0 혹은 1로 시작하는 수의 집합으로 각각의 수는 이 전의 2수의 합한 수와 같습니다.

```javascript
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...
```

혹은

```javascript
1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...
```

문제는 수열 안에 n번 째 요소의 값을 리턴하는 것 입니다.

```javascript
[1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...]
```

```javascript
function fibonacci(n) {
  if (n == 1 || n == 2) {
    return 1;
  }
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```

간결하고 정확하지만 여기에는 문제가 있습니다. 재귀함수를 사용하고 있기때문에 동일한 함수호출이 반복적으로 이뤄지고 있습니다. 아래 fib(5)가 호출되었을 때의 다이어그램을 보면 각각 다른 브런치에서 반복적으로 동일한 피보나치의 값을 찾으려고 노력합니다. 이것은 중족계산이고 memoization이 필요한 이유입니다.

```javascript
function fibonacci(n, memo) {
  memo = memo || {};
  if (memo[n]) {
    return memo[n];
  }
  if (n == 0 || n == 1) {
    return 1;
  }
  return (memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo));
}
```
