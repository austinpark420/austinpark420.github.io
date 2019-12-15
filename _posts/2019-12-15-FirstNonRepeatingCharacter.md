---
layout: post
title: 알고리즘 - First non-repeating character
permalink: posts/FirstNonRepeatingCharacter

tag: algorithm
---

## 문제

Write a function named first_non_repeating_letter that takes a string input, and returns the first character that is not repeated anywhere in the string.

For example, if given the input 'stress', the function should return 't', since the letter t only occurs once in the string, and occurs first in the string.

As an added challenge, upper- and lowercase letters are considered the same character, but the function should return the correct case for the initial letter. For example, the input 'sTreSS' should return 'T'.

If a string contains all repeating characters, it should return an empty string ("") or None -- see sample tests.

## 풀이과정

1. 이중 for문을 활용한다.
2. 외부 for문은 기준이 되는 문자열이고 안에 for문을 기준이 되는 문자열이 중복이 되는지 확인하는 for문이다.
3. 중복을 체크하는 문자열을 확인하는 nonRepeat이라는 변수를 생성한다.
4. 중복이 되지 않는 문자열을 반환하고 중복되지 않는 문자열이 있다면 ''을 반환한다.

### code

```javascript
function firstNonRepeatingLetter(s) {
  for (var i = 0; i < s.length; i++) {
    var nonRepeat = true;
    for (var j = 0; j < s.length; j++) {
      if (i === j) continue;
      if (s[i].toUpperCase() === s[j].toUpperCase()) nonRepeat = false;
    }

    if (nonRepeat) return s[i];
  }

  return '';
}
```

### 출처: [www.codewars.com](https://www.codewars.com)
