---
layout: post
title: 시간 복잡도(Time Complexity)
permalink: posts/timeComplexity
tag: javascript
---

> 해당 포스트는 [Time Complexity Analysis in JavaScript](https://www.jenniferbland.com/time-complexity-analysis-in-javascript/)를 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

알고리즘은 문제를 해결하기위해 그들만의 절차를 가지고 있습니다. 이러한 절차에 따라서 실행되는 시간이 결정됩니다. 알고리즘을 해결하기 위해 필요한 시간은 시간 복잡도로 알려져 있습니다.

여기에 공식적인 시간 복잡도 정의가 있습니다. 알고리즘의 시간복잡도는 입력값을 나타내는 문자의 길이로 함수를 실행하는데 걸리는 시간을 뜻합니다.

시간복잡도는 알고리즘이 요구하는 시간과 공간으로 정의됩니다.

많은 문제를 풀기위해서 찾아야하는 방법으로 시간적합도는 일반적이지 않을 수 있습니다.

시간의 길이와 명령들은 효과적으로 문제를 풀기위해서 사용됩니다. 복잡도는 개발자들의 이해를 돕기때문에 코드를 개선하고 효율적으로 만들 수 있습니다.

자바스크립트에서 효과적인 프로그래밍 솔루션은 가능하한 낮은 시간 복잡도를 통해 알고리즘을 설계하는 것입니다.

## Big O Notation

알고리즘의 시간복잡도는 흔히 Big O Notation을 이용해서 표현됩니다. Big O Notation은 실행시간이나 알고리즘에 사용되는 공간으로 정의됩니다. Big O Notation은 보통 가장 안 좋은 시나리오를 설명할 수 있습니다.

앞서 언급했다드시피 문제가 복잡해지고 길어질 수록 알고리즘을 해결하는데 더 많은 시간이 소요될 겁니다.

문제가 복잡해지면 복잡해질수록 비용은 빠르게 증가, 감소 혹은 거의 증가하지 않을 수 있습니다.. Big O Notation은 얼마나 빠르게 문제를 해결하는지 측정하는데 사용됩니다.

아래의 그래프는 각각의 Big O Notation 레벨을 보여주고 있으며 동작이 증가할수록 알고리즘을 해결하는데 소요되는 시간을 상대적으로 보여주고 있습니다.
![Big O Notation Complexity](https://i1.wp.com/www.jenniferbland.com/wp-content/uploads/big-o-complexity.png?w=783&ssl=1)

### O(1) - 일정한 시간복잡도

Big O Notation에서 가장 빠른 시간 복잡도를 일정한 시간 복잡도라고 이야기합니다. O(1)의 값이 주어집니다. 일정한 시간 복잡도를 이용하면 복잡한 문제를 입력한다고 해도 계산을 하는데 동일한 시간이 소요됩니다. 일정한 시간복잡도는 자바스크립트 함수에서 베스트 시나리오로 여겨집니다.
![Constant Time Complexity](https://i0.wp.com/www.jenniferbland.com/wp-content/uploads/O1-constant-time-complexity.jpg?w=416&ssl=1)

### O(log n) – 로그(Logarithmic)

로그 시간복잡도는 실행시간은 점점 증가하지만 증가하는 비율은 감소합니다.

여기에 로그 검색에 대한 좋은 예가 있습니다. 100만개의 이름이 있는 전화번호부에 특정 이름을 검색하고 싶다고 가정해 봅시다.

먼저 50만번을 기준으로 찾고 있는 이름이 있는지 비교해 봅니다. 중간 지점의 이름이 찾고있는 알파벳보다 낮으면 계속해서 진행합니다.

50만 번째 이름과 찾으려고하는 이름을 비교합니다. 알파벳 순서에 따라 동일한 일은 위 혹은 아래로 반복적으로 실행하면서 이름을 검색합니다.

만약에 전화번호부에 3개의 이름만 존재한다면 원하는 이름을 찾는데 많아야 2번 검색하면 됩니다.

만약에 전화번호부에 15개의 이름이 있다면 원하는 이름을 찾는데 4번을 검색하면 됩니다.

백 만개의 이름이 있는 전화번호에서는 많아야 20번을 검색하면 됩니다.

시간복잡도는 계속 증가하지만 입력값이 증가하는 만큼 빠르게 증가하지는 않습니다.

![O(log n) – 로그(Logarithmic)](https://i1.wp.com/www.jenniferbland.com/wp-content/uploads/Olog-n-logarithmic-complexity.jpg?w=472&ssl=1)

### O(n) - 선형(Linear)

O(n)은 알고리즘의 퍼포먼스가 선형으로 증가하고 입력 값의 정비례하게 증가합니다.

요소가 10개인 배열을 프린트하고 싶다고 가정해 봅시다. 각 요소를 순회하면서 출력을 해야합니다.

만약 배열에 100개의 요소가 있다면 100번 순회를 해야합니다.

100만개라면 100만번을 순회해야합니다.

시간복잡도를 보면 입력 값의 크기만큼 동일한 비율로 실행시간이 증가합니다.

![O(n) - 선형(Linear)](https://i2.wp.com/www.jenniferbland.com/wp-content/uploads/On-Linear-Complexity.jpg?w=463&ssl=1)

### O(n2) – 제곱(Quadratic)

제곱 시간복잡도는 로그표기법과 거의 반대입니다. 제곱 시간복잡도를 이용하면 입력 값에 비해 긴 시간이 소요됩니다.

제곱 시간복잡도는 함수의 실행이 입력 값의 제곱에 비례합니다. 제곱 시간은 전형적으로 ‘order N squared’ 혹은 O(n^2)이라고 표시합니다. 이 표기법은 O(1)과 O(n)을 동작시키기위해서 사용합니다.

![O(n2) – 제곱(Quadratic)](https://i1.wp.com/www.jenniferbland.com/wp-content/uploads/On2-quadratic-time-complexity.jpg?w=382&ssl=1)
