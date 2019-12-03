---
layout: post
title: 알고리즘 - The Hashtag Generator
permalink: posts/TheHashtagGenerator
tag: algorithm
---

## 문제

The marketing team is spending way too much time typing in hashtags.
Let's help them with our own Hashtag Generator!

Here's the deal:

It must start with a hashtag (#).
All words must have their first letter capitalized.
If the final result is longer than 140 chars it must return false.
If the input or the result is an empty string it must return false.

### 예시

```javascript
" Hello there thanks for trying my Kata"  =>  "#HelloThereThanksForTryingMyKata"
"    Hello     World   "                  =>  "#HelloWorld"
""                                        =>  false
```

## 풀이과정

1. 빈 문자열일 때 false
2. 결과물을 담을 변수에 우선 #을 할당
3. 문자열을 수회할 때 순회하는 문자열 빈 문자열이면 continue, 순회하는 문자열 앞에 빈 문자열이거나 첫번째 문자열이면 해당 문자를 대문자로 변환

### code

```javascript
function generateHashtag(str) {
  if (str.trim().length === 0) return false;

  var result = '#';

  for (var i = 0; i < str.length; i++) {
    if (str[i] === ' ') continue;
    else if (str[i - 1] === ' ' || i === 0) result += str[i].toUpperCase();
    else result += str[i];
  }

  if (result.length > 140) return false;
  else return result;
}
```

### 출처: [www.codewars.com](https://www.codewars.com)
