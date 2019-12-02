---
layout: post
title: 알고리즘 - Where my anagrams at?
permalink: posts/whereMyAnagramsAt
tag: algorithm
---

## 문제

What is an anagram? Well, two words are anagrams of each other if they both contain the same letters. For example:

```javascript
'abba' & ('baab' == true);

'abba' & ('bbaa' == true);

'abba' & ('abbba' == false);

'abba' & ('abca' == false);
```

Write a function that will find all the anagrams of a word from a list. You will be given two inputs a word and an array with words. You should return an array of all the anagrams or an empty array if there are none. For example:

```javascript
anagrams('abba', ['aabb', 'abcd', 'bbaa', 'dada']) => ['aabb', 'bbaa']

anagrams('racer', ['crazer', 'carer', 'racar', 'caers', 'racer']) => ['carer', 'racer']

anagrams('laser', ['lazing', 'lazy',  'lacer']) => []
```

## 풀이과정

1. 주어진 word의 알파벳 숫자와 words 요소의 알파벳 숫자가 동일한 요소를 출력해야함.
2. filter를 사용해서 word의 알파벳과 words 요소의 알파벳을 정렬한다.
3. 정렬한 값을 비교해서 word와 동일하게 정렬된 words의 요소를 출력한다.

### code

```javascript
function anagrams(word, words) {
  return words.filter(
    item =>
      item
        .split('')
        .sort()
        .join('') ===
      word
        .split('')
        .sort()
        .join('')
  );
}
```

### 출처: [www.codewars.com](https://www.codewars.com)
