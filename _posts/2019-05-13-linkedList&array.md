---
layout: post
title: linked list와 array의 차이
permalink: posts/linkedListVSarray
tag: javascript array linkedList
---

> 해당 포스트는 [Linked List vs Array](https://www.geeksforgeeks.org/linked-list-vs-array/)를 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

array와 linked list는 비슷한 타입의 선형 데이터를 저장하는 데 사용됩니다. 그러나 각각의 장단점이 있습니다.

## Array와 Linked list의 차이점

1. Array는 비슷한 타입의 요소를 모아놓은 데이터구조이고, Linked List는 순서가 정해지인 않은 노드로 연결된 요소들의 집합으로 이루어진 데이터 구조입니다.
2. Array안에 있는 요소들은 인덱스를 가지고 있습니다. 예를 들어 네번 째 요소에 접근하기 위해서 변수 이름과 함께 인덱스를 작성하거나 대괄호안에 인텍스를 작성하면 됩니다.
3. Linked List는 네번 째 요소에 접근하기위해서는 첫번 쩨 요소를 통해서 순차적으로 접근해야합니다.
4. 요소에 접근하는 속도는 Array가 빠르지만, Linked List는 Array보다 상대적으로 느립니다.
5. 요소를 추가하거나 제거하는데 Array는 오랜 시간이 걸립니다. 반며에 Linked List는 빠릅니다.
6. Array는 크기가 고정되어 있지만 Linked List는 크기가 유동적이고 요소의 크기만큼 확장할 수 있습니다.
7. Array의 경우, 메모리가 컴파일할 때 할당되지만 Linked List는 실행 혹은 런타임시에 메모리에 할당됩니다.
8. Array 안에서 순차적으로 저장되지만, Linked List는 랜덤으로 저장됩니다.
9. Array의 경우, 요소가 array의 인덱스에 저장되기때문에 메모리 요구사항이 작지만, Linked List는 이전과 이후의 참조를 함께 저장해야하기 때문에 상대적으로 메모리를 차지하는 양이 큽니다.
10. 추가적인 메모리 사용은 Array에서는 비효율적이지만 Linked List에서는 효율적입니다.
