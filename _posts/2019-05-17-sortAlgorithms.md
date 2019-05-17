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
function bubbleSort(arr){
    len = arr.length;
    for(var i = len-1; i >= 0; i--) {
        fort(j = 1; j <= i; i++){
            if(arr[j-1] > arr[j]){
                var temp = arr[j-1];
                arr[j-1] = arr[j];
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
