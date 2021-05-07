---
title: "[Swift] 프로그래머스 lv1 두 정수 사이의 합"
excerpt: "연습문제 lv1"

categories:
  - 프로그래머스
tags:
  - swift
  - 프로그래머스
  - 알고리즘
  - 코딩테스트
---

```swift
func solution(_ a:Int, _ b:Int) -> Int64 {
    var result = a > b ? Array(b...a).reduce(0, +) : Array(a...b).reduce(0, +)
    return Int64(result)
  }
```
처음에 고차함수를 활용해서 풀었더니 4번문제에서 시간 초과가 나와서 한참 생각하다 반복문으로 해보니 통과...
<br></br>
```swift
func solution(_ a:Int, _ b:Int) -> Int64 {
    var result = 0

    for num in a>b ? b...a : a...b {
        result += num
    }

    return Int64(result)
}
```

범위 안에서도 조건문을 사용할 수 있다.
제한 조건을 잘 보자.
연속된 값의 경우 반복문을 생각하자.