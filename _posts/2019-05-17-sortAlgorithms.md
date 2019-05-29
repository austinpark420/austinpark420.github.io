---
layout: post
title: 정렬 알고리즘(sort algorithms)
permalink: posts/sortAlgorithms
tag: javascript sort algorithms
---

> 해당 포스트는 [JS: Interview Questions](https://khan4019.github.io/front-end-Interview-Questions/sort.html)를 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

## Bubble Sort

동작 방법

- step 1. 첫 번째 아이템을 두 번째 아이템과 비교합니다. 만약 첫 번째 아이템이 크다면 서로 위치를 바꿉니다.
- step 2. 두 번째 아이템과 세 번째 아이템을 비교합니다. 두 번째 아이템이 크다면 서로 위치를 바꿉니다. 그렇지 않으면 그대로 내버려둡니다. 그래서 처음 세 번째 까지 아이템 중에 가장 큰 아이템이 세 번째 위치하게 됩니다.
- step 3. 마지막 배열의 아이템까지 계속해서 반복합니다. 이러한 방법으로 가장 큰 아이템이 배열의 오른쪽에 위치하도록 버블링 합니다.
- step 4. 아래의 안에 있는 반복문을 확인해 보세요.
- step 5. 이러한 코드를 반복적으로 실행합니다. 밖에 있는 반복문을 확인해 보세요. 첫 번째 안에 있는 반복문을 끝나면 큰 아이템을 배열의 오른쪽에 위치됩니다.
- step 6. 그 다음에 다시 안에 있는 반복문으로 들어가게됩니다.

```javascript
function bubbleSort(arr) {
  len = arr.length;
  for (var i = len - 1; i >= 0; i--) {
    for (j = 1; j <= i; j++) {
      if (arr[j - 1] > arr[j]) {
        var temp = arr[j - 1];
        arr[j - 1] = arr[j];
        arr[j] = temp;
      }
    }
  }
  return arr;
}
```

## selection sort

동작 원리: 정말 간단합니다. 배열을 통해 가장 낮은 요소를 찾고 첫 번째 요소와 위치를 변경합니다. 그러면 가장 작은 요소는 배열의 첫 번째에 위치힙니다.  
다음으로 첫 번째 인덱스를 제외하고 가장 작은 요소를 찾고 두 번째 인덱스에 위치시킵니다.  
이것은 배열에서 가장 작은 요소를 찾고 배열의 왼쪽부터 위치시키는 것입니다.

![selection sort img](https://khan4019.github.io/front-end-Interview-Questions/images/selectionSort.png)

```javascript
function selectionSort(arr) {
  var minIdx, temp;
  var len = arr.length;
  for (var i = 0; i < len; i++) {
    minIdx = i;
    for (var j = i + 1; j < len; j++) {
      if (arr[j] < arr[minIdx]) {
        minIdx = j;
      }
    }
    temp = arr[i];
    arr[i] = arr[minIdx];
    arr[minIdx] = temp;
  }
  return arr;
}
```

## Insertion sort

동작 원리: 카드를 하고 있다고 상상해보세요. 누군가가 카드 한 장씩 전달해줍니다. 카드를 받았을 때 비슷한 카드끼리 모아두려고 정리를해서 왼쪽부터 놓으려고 계획합니다. 즉 정렬된 방식으로 삽입하는 것을 뜻합니다.

- step 1. 첫 번째 카드로 5번을 전달 받았습니다. 우선 카드를 손에 두고 아무런 행동을 취하지 않습니다.
- step 2. 만약 두 번째 카드가 2번이면, 카드를 정렬하기위해서 카드 5번 왼쪽으로 2번을 정렬시킵니다. 2번 카드를 왼쪽으로 정렬했을 때 5번 카드는 첫 번째 포지션이에 두 번째 포지션으로 변경됩니다. 그리고 첫 번째 포지션을 활용가능하고 2번을 첫 번째 포지션으로 변경합니다.
- step 3. 세 번째 카드가 4번이면 두 번째 포지션에서 시작할 수 있습니다. 두 번째 포지션으로는 4보다 큰 5번을 가지고 있습니다. 그래서 5번을 세 번째 포지션으로 옮깁니다. 왼 쪽에 있는 4번보다 작은 2번입니다. 그래서 2번을 옮기고 4번을 두 번째 포지션으로 삽입합니다.
- step 4. 10번을 전달받았습니다. 10번은 이전에 전달받은 5번보다 큽니다. 그래서 맨 마지막 포지션에 삽입합니다.
- step 5. 다음 카드는 7번 입니다. 10번을 마지막 포지션으로 옮기고 7번을 삽입합니다.
- step 6. 마지막 카드는 3번 입니다. 10번 카드는 3보다 크기때문에 마직막 포지션으로 이동시킵니다. 그 다음에 3보다 큰 7번을 확인하고 오른쪽으로 이동시킵니다. 비슷하게 이러한 과정으로 5,4번의 포지션을 이동시킵니다. 3번을 2번 오른쪽에 위치시킵니다.
  ![Insertion sort img](https://khan4019.github.io/front-end-Interview-Questions/images/insertionSort.png)

### insertion sort code

코드는 위에 있는 이미지와 카드와 비슷합니다. 두 번째 요소부터 시작합니다. 삽입된 두 번째 요소를 선택하고 이전의 요소와 비교를 합니다. 만약 첫 번째 요소가 크다면 첫 번째 요소를 두 번째 포지션으로 옮기고 두번째 요소를 첫 번째 포지션으로 이동시킵니다.

이제 첫 번째, 두 번째 요소가 정렬되었습니다.

그리고 세 번째 요소를 선택하고 두 번째 요소와 크기를 비교합니다. 이러한 방법으로 계속 진행합니다. 선택한 항목보다 작은 아이템을 가져오면 해당 항목을 삽입합니다.

```javascript
function insertionSort(arr) {
  var len = arr.length;

  for (var i = 1; i < len; i++) {
    var el = arr[i];
    var j = i;

    while (j > 0 && arr[j - 1] > el) {
      arr[j] = arr[j - 1];
      j--;
    }
    arr[j] = el;
  }
  return arr;
}
```

## Merge Sort

이것은 나누고 획득하는 알고리즘입니다.  
배열을 하나의 작은 단위로 나누고 그것들을 비교하면서 합쳐나갑니다. 만약 아직도 제(필자)가 하는 이야기가 이해되지 않는다면 위키피디아에서 가져온 아래의 이미지를 확인해보세요.

![merge sort image](https://khan4019.github.io/front-end-Interview-Questions/images/mergeSort.gif)

code merge sort: 머지 소트는 2개의 파트가 있습니다. 메인 파트는 나누는 파트이고 두 번째 파트는 합치는 파트입니다.
divide: mergeSort의 첫 번째 함수는 나누는 함수입니다.
merge: 나눠진 배열을 합치는 것입니다. 두 배열이 크기가 다를 수 있다는 것을 주의하시기 바랍니다.

```javascript
function mergeSort(arr) {
  var len = arr.length;
  if (len < 2) return arr;
  var mid = Math.floor(len / 2),
    left = arr.slice(0, mid),
    right = arr.slice(mid);
  return merge(mergeSort(left), mergeSort(right));
}
```

```javascript
function merge(left, right) {
  var result = [],
    lLen = left.length,
    rLen = right.length,
    l = 0,
    r = 0;
  while (l < lLen && r < rLen) {
    if (left[l] < right[r]) {
      result.push(left[l++]);
    } else {
      result.push(right[r++]);
    }
  }

  return result.concat(left.slice(l)).concat(right.slice(r));
}
```

## Quick sort

### 동작 원리

- step1: 피봇을 선택해야합니다. 랜덤으로 선택되거나 중간 지점입니다. 여기서 우리는 마지막 배열의 요소를 선택합니다.
- step2: 피봇을 기준으로 작은 수는 왼쪽에 큰 수는 오른쪽에 배치합니다.
- step3: step2를 반복적으로 실행합니다.

### 코드 예시

- 퀵 소트 호출: 배열을 전달하고 퀵 소트 함수에 왼쪽 오른쪽에 전달합니다. 첫 번째 호출에서 left는 첫 번째 요소의 인덱스가 0이고 right는 마자막 요소의 인덱스가 -1입니다.
- 피봇 선택: 배열의 마지막 인덱스를 피봇으로 선택합니다.
- 파디션 함수 호출: 파티션 함수에서 피봇보다 작은 수를 왼쪽에 큰 수를 오른쪽에 배치합니다. 우리는 파티션의 위치를 추적해야합니다. 그러기위해서는 다음 스텝에서 배열을 2개로 나눌 수 있습니다. 배열을 분열하는 인덱스를 추적하는 것은 partitionindex 변수를 사용해서 수행됩니다. 초기값은 왼쪽에 있습니다.
- swap function: 배열의 값을 교환할 때 도움을 주는 함수입니다.
- move elements: 왼쪽부터 반복문을 실행합니다. 그리고 값이 피봇값보다 작으면 partitionindex를 바꾸고 partitionindex 값을 늘립니다. 만약 값이 크다면 아무 것도 하지 않습니다. 마지막 요소까지 같은 일은 반복합니다.(마지막 요소가 피봇이라는 것을 기억하세요)
- place pivot: 작은 요소를 왼쪽으로 모두 이동시켰다면 마지막 요소(피봇 값)을 patitionindex와 함께 교환합니다.
- repeat the process: 다시 퀵 소트 함수로 돌아와서 partitionindex를 활용해서 배열의 왼쪽, 오른쪽 사이드에 각각 적용합니다.

```javascript
function quickSort(arr, left, right) {
  var len = arr.length,
    pivot,
    partitionIndex;

  if (left < right) {
    pivot = right;
    partitonIndex = partition(arr, pivot, left, right);

    quickSort(arr, left, partitionIndex - 1);
    quickSort(arr, partitionIndex + 1, right);
  }
  return arr;
}

function partition(arr, pivot, left, right) {
  var pivotValue = arr[pivot],
    partitionIndex = left;

  for (var i = left; i < right; i++) {
    if (arr[i] < pivotValue) {
      swap(arr, i, partitionIndex);
      partitionIndex++;
    }
  }
  swap(arr, right, partitionIndex);
  return partitionIndex;
}

function swap(arr, i, j) {
  var temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
}
```

![quickSort image](https://khan4019.github.io/front-end-Interview-Questions/images/quickSort.png)
