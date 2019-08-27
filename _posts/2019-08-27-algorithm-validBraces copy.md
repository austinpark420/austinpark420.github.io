---
layout: post
title: 알고리즘 - IQ Test
permalink: posts/iqTest
tag: [algorithm]
---
## 문제
Bob is preparing to pass IQ test. The most frequent task in this test is to find out which one of the given numbers differs from the others. Bob observed that one number usually differs from the others in evenness. Help Bob — to check his answers, he needs a program that among the given numbers finds one that is different in evenness, and return a position of this number.

! Keep in mind that your task is to help Bob solve a real IQ test, which means indexes of the elements start from 1 (not 0)

### 예시
```javascript
iqTest("2 4 7 8 10") => 3 // Third number is odd, while the rest of the numbers are even

iqTest("1 2 1 1") => 2 // Second number is even, while the rest of the numbers are odd
```

## 풀이과정

1. 입력받는 숫자를 순회하면서 홀수와 짝수을 가려내야한다.
2. 홀수와 짝수 중 유일한 값의 위치를 반환해야한다.
3. 위치 값을 배열에 담는다.
4. 배열의 길이를 이용하면 위치값을 리턴한다.

### code
```javascript
function iqTest(numbers) {
  let odd = [];
  let even = [];
  let numbersArray = numbers.split(' ');

  for (let i = 0; i < numbersArray.length; i++){
    if (Number(numbersArray[i]) % 2 === 0) {
      even.push(i + 1);
    } else {
      odd.push(i + 1);
    }
  }

  if(even.length === 1) {
    return even[0];
  } else {
    return odd[0];
  }
}
```

### 출처: [www.codewars.com](https://www.codewars.com)