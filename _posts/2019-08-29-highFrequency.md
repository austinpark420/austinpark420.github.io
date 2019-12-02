---
layout: post
title: 알고리즘 - High frequency String
permalink: posts/highFrequency
tag: algorithm
---

## 문제

입력받은 문자열에서 빈도수가 가장 많은 알파벳을 반환하세요. 만약 빈도가 같은 알파벳이 있다면 먼저 나온 알파벳을 반환하세요.

### 예시

```javascript
highFrequency('aabbbccc'); // Should return 'b'
highFrequency('aabbbcccc'); // Should return 'c'
```

## 풀이과정

1. 각 알파벳의 갯수를 파악해야 함.
2. 파악한 알파벳의 갯수를 비교해야함.
3. 이중 for문을 사용해서 밖에 있는 for문에 순회하는 알파벳의 갯수를 currentStringNumber에 저장
4. highFrequencyStringNumber 와 currentStringNumber를 비교해 highFrequencyStringNumber의 값을 변경 혹은 유지함.

### code

```javascript
function highFrequency(string) {
  let result = '';
  let highFrequencyStringNumber = 0;
  let currentStringNumber = 0;

  for (let i = 0; i < string.length; i++) {
    let counter = 1;

    for (let j = i + 1; j < string.length; j++) {
      if (string[i] === string[j]) counter++;
    }

    currentStringNumber = counter;

    if (currentStringNumber > highFrequencyStringNumber) {
      highFrequencyStringNumber = currentStringNumber;
      result = string[i];
    }
  }

  return result;
}
```

### 출처: [www.codewars.com](https://www.codewars.com)
