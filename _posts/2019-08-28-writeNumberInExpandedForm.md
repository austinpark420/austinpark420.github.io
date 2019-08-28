
---
layout: post
title: write Number in Expanded Form
permalink: posts/writeNumber
tag: algorithm
---
## 문제
You will be given a number and you will need to return it as a string in Expanded Form. For example:

### 예시
```javascript
expandedForm(12); // Should return '10 + 2'
expandedForm(42); // Should return '40 + 2'
expandedForm(70304); // Should return '70000 + 300 + 4'
```

## 풀이과정

1. 입력받는 숫자를 뒤에서부터 순회한다.
2. 순회하는 숫자의 특정 자릿수 값이 0일 경우 Pass
3. 순회하는 숫자의 특정 자릿수 값이 0이 아닐 경우 자릿수의 값을 계산한다.

### code
```javascript
function iqTest(numbers) {
  let result;
  let digit = 0;
  let numToString = num.toString();

  for(let i = numToString.length - 1 ; i >= 0; i--) {
    if (numToString[i] != 0) {
      if (!result) {
        result = numToString[i] * Math.pow(10, digit);
      } else {
        result = numToString[i] * Math.pow(10, digit) + ' + ' + result;
      }
    }
    digit++;
  }

  return result.toString();
}
```

### 출처: [www.codewars.com](https://www.codewars.com)