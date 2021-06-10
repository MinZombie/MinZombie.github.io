---
title: "[Swift] enumerated로 배열의 인덱스 값 구하기"

categories:
  - swift
tags:
  - swift
  - enumerated
---
알고리즘 문제를 풀다가 다른 사람의 풀이를 봤는데 enumerated()라는 함수를 사용했다. 몰라서 찾아보니 반복문을 사용하면서 그 요소의 인덱스 값을 알고 싶을 때 enumerated()를 사용한다고 이해하면 쉽다.

```swift
var arr: [String] = ["A", "B", "C", "D", "E"]
for (index, value) in arr.enumerated() {
    print("\(index) : \(value)")
}
/*
0 : A
1 : B
2 : C
3 : D
4 : E
*/
```