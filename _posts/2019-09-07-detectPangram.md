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

1. 주어진 word의 알파벳 숫자와 words 요소의 알파벳 숫자가 동일한 요소를 출력해야함.
2. filter를 사용해서 word의 알파벳과 words 요소의 알파벳을 정렬한다.
3. 정렬한 값을 비교해서 word와 동일하게 정렬된 words의 요소를 출력한다.

### code

```javascript
function isPangram(string) {
  const alphabet = "abcdefghijklmnopqrstuvwxyz";

  const isInclude = element => {
    return string.toLowerCase().split("").includes(element);
  };

  return alphabet.split("").every(isInclude);

}
```
