---
layout: post
title: 알고리즘 - Human readable duration format
permalink: posts/HumanReadableDurationFormat
tag: algorithm
---

## 문제

Your task in order to complete this Kata is to write a function which formats a duration, given as a number of seconds, in a human-friendly way.

The function must accept a non-negative integer. If it is zero, it just returns "now". Otherwise, the duration is expressed as a combination of years, days, hours, minutes and seconds.

Note that spaces are important.

Detailed rules
The resulting expression is made of components like 4 seconds, 1 year, etc. In general, a positive integer and one of the valid units of time, separated by a space. The unit of time is used in plural if the integer is greater than 1.

The components are separated by a comma and a space (", "). Except the last component, which is separated by " and ", just like it would be written in English.

A more significant units of time will occur before than a least significant one. Therefore, 1 second and 1 year is not correct, but 1 year and 1 second is.

Different components have different unit of times. So there is not repeated units like in 5 seconds and 1 second.

A component will not appear at all if its value happens to be zero. Hence, 1 minute and 0 seconds is not valid, but it should be just 1 minute.

A unit of time must be used "as much as possible". It means that the function should not return 61 seconds, but 1 minute and 1 second instead. Formally, the duration specified by of a component must not be greater than any valid more significant unit of time.

### 예시

```javascript
formatDuration(62); // returns "1 minute and 2 seconds"
formatDuration(3662); // returns "1 hour, 1 minute and 2 seconds"

// For the purpose of this Kata, a year is 365 days and a day is 24 hours.
```

## 풀이과정

1. 년, 일, 분, 초를 구분하기
2. 파라미터 seconds를 순차적으로 년, 일, 분, 초의 값으로 나누기
3. 복수, 단수 값을 처리하기
4. 년, 일, 분, 초의 수에 따라 'and', ','의 값 할당하기

### code

```javascript
function formatDuration(seconds) {
  if (seconds === 0) return 'now';

  const year = 60 * 60 * 24 * 365;
  const day = 60 * 60 * 24;
  const hour = 60 * 60;
  const minute = 60;
  const second = 1;

  let temp = 1;
  let tempArray = [];
  let result = '';

  if (seconds >= year) {
    temp = Math.floor(seconds / year);
    if (temp > 1) {
      tempArray.push(`${temp} years`);
    } else {
      tempArray.push(`${temp} year`);
    }
    seconds = seconds - temp * year;
  }
  if (seconds >= day) {
    temp = Math.floor(seconds / day);
    if (temp > 1) {
      tempArray.push(`${temp} days`);
    } else {
      tempArray.push(`${temp} day`);
    }
    seconds = seconds - temp * day;
  }
  if (seconds >= hour) {
    temp = Math.floor(seconds / hour);
    if (temp > 1) {
      tempArray.push(`${temp} hours`);
    } else {
      tempArray.push(`${temp} hour`);
    }
    seconds = seconds - temp * hour;
  }
  if (seconds >= minute) {
    temp = Math.floor(seconds / minute);
    if (temp > 1) {
      tempArray.push(`${temp} minutes`);
    } else {
      tempArray.push(`${temp} minute`);
    }
    seconds = seconds - temp * minute;
  }
  if (seconds >= second) {
    temp = Math.floor(seconds / second);
    if (temp > 1) {
      tempArray.push(`${temp} seconds`);
    } else {
      tempArray.push(`${temp} second`);
    }
  }

  if (tempArray.length > 2) {
    for (let i = 0; i < tempArray.length; i++) {
      if (i < tempArray.length - 2) {
        result += tempArray[i] + ', ';
      } else if (i === tempArray.length - 2) {
        result += tempArray[i] + ' and ';
      } else {
        result += tempArray[i];
      }
    }
  } else if (tempArray.length === 2) {
    for (let i = 0; i < tempArray.length; i++) {
      if (i === 0) {
        result += tempArray[i] + ' and ';
      } else {
        result += tempArray[i];
      }
    }
  } else {
    result += tempArray[0];
  }

  return result;
}
```

### 출처: [www.codewars.com](https://www.codewars.com)
