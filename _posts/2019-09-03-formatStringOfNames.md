---
layout: post
title: 알고리즘 - Format a string of names
permalink: posts/formatStringOfNames
tag: algorithm
---

## 문제

Given: an array containing hashes of names

Return: a string formatted as a list of names separated by commas except for the last two names, which should be separated by an ampersand.

### 예시

```javascript
list([{ name: 'Bart' }, { name: 'Lisa' }, { name: 'Maggie' }]);
// returns 'Bart, Lisa & Maggie'

list([{ name: 'Bart' }, { name: 'Lisa' }]);
// returns 'Bart & Lisa'

list([{ name: 'Bart' }]);
// returns 'Bart'

list([]);
// returns ''
```

## 풀이과정

1. 홀수만 골라서 정렬해야 함
2. 정렬방법 중 selection sort가 적합하다고 판단

### code

```javascript
function list(names) {
  let result;

  if (!names.length) return (rusult = '');
  else if (names.length == 1) return (result = names[0].name);

  for (let i = 0; i < names.length; i++) {
    if (!result) {
      result = names[i].name;
    } else if (i === names.length - 1) {
      result += ' & ' + names[i].name;
    } else {
      result += ', ' + names[i].name;
    }
  }

  return result;
}
```

### 출처: [www.codewars.com](https://www.codewars.com)
