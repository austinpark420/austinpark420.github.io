---
layout: post
title: 알고리즘 - Valid Braces
permalink: posts/validBraces
tag: [algorithm]
---
## 문제
Write a function that takes a string of braces, and determines if the order of the braces is valid. It should return true if the string is valid, and false if it's invalid.

This Kata is similar to the Valid Parentheses Kata, but introduces new characters: brackets [], and curly braces {}. Thanks to @arnedag for the idea!

All input strings will be nonempty, and will only consist of parentheses, brackets and curly braces: ()[]{}.

What is considered Valid?
A string of braces is considered valid if all braces are matched with the correct brace.

```javascript
Examples
"(){}[]"   =>  True
"([{}])"   =>  True
"(}"       =>  False
"[(])"     =>  False
"[({})](]" =>  False
```

## 풀이과정

1. braces의 갯수를 체크하기 (여는 태그와 닫는 태그의 짝이 맞아야한다.)
2. 모든 braces는 여는 태그로 시작해야 한다.

### code
```javascript
function validBraces(braces) {
  let parenthesis = 0;
  let brace = 0;
  let squareBracket = 0;

  for (let i = 0; i < braces.length; i++) {
    if (braces[i] === '(') parenthesis++;
    if (braces[i] === '{') brace++;
    if (braces[i] === '[') squareBracket++;

    if (braces[i] === ')') {
      if (parenthesis === 0) {
        return false;
      } else {
        parenthesis--;
      }
    }
    if (braces[i] === '}') {
      if (brace === 0) {
        return false;
      } else {
        brace--;
      }
    }
    if (braces[i] === ']') {
      if (squareBracket === 0) {
        return false;
      } else {
        squareBracket--;
      }
    }
  }

  if (parenthesis === 0 && brace === 0 && squareBracket === 0) {
    return true;
  } else {
    return false;
  }
}
```

### 출처: [www.codewars.com](https://www.codewars.com)