---
layout: post
title: 알고리즘 - Perimeter of squares in a rectangle
permalink: posts/PerimeterOfSquaresInARectangle
tag: algorithm
---

## 문제

The drawing shows 6 squares the sides of which have a length of 1, 1, 2, 3, 5, 8. It's easy to see that the sum of the perimeters of these squares is : 4 _ (1 + 1 + 2 + 3 + 5 + 8) = 4 _ 20 = 80

Could you give the sum of the perimeters of all the squares in a rectangle when there are n + 1 squares disposed in the same manner as in the drawing:

alternative text

#Hint: See Fibonacci sequence

#Ref: http://oeis.org/A000045

The function perimeter has for parameter n where n + 1 is the number of squares (they are numbered from 0 to n) and returns the total perimeter of all the squares.

### 예시

```javascript
perimeter(5)  should return 80
perimeter(7)  should return 216
```

## 풀이과정

1. 피보나치 수열 함수를 생성
2. 피보나치 수열의 값들의 합에 4를 곱한 값을 리턴

### code

```javascript
function fibonacci(n) {
  var a = 1,
    b = 0,
    temp;

  while (n >= 0) {
    temp = a;
    a = a + b;
    b = temp;
    n--;
  }

  return b;
}

function perimeter(n) {
  var sum = 0;

  for (var i = n; i >= 0; i--) {
    sum += fibonacci(i);
  }

  var result = sum * 4;
  return result;
}
}
```

### 출처: [www.codewars.com](https://www.codewars.com)
