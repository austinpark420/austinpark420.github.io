---
layout: post
title: 알고리즘 - Detect Pangram
permalink: posts/detectPangram
tag: algorithm
---

## 문제

A pangram is a sentence that contains every single letter of the alphabet at least once. For example, the sentence "The quick brown fox jumps over the lazy dog" is a pangram, because it uses the letters A-Z at least once (case is irrelevant).

Given a string, detect whether or not it is a pangram. Return True if it is, False if not. Ignore numbers and punctuation.

## 풀이과정

1. 알파벳을 식별할 수 있는 변수를 생성한다.
2. 주어진 문자열을 순회하면서 알파벳을 포함하는지 확인한다.

### code

```javascript
function isPangram(string) {
  const alphabet = 'abcdefghijklmnopqrstuvwxyz';

  const isInclude = element => {
    return string
      .toLowerCase()
      .split('')
      .includes(element);
  };

  return alphabet.split('').every(isInclude);
}
```

### 출처: [www.codewars.com](https://www.codewars.com)
