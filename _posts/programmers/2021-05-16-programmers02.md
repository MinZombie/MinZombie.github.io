---
title: "[Swift] 프로그래머스 lv1 약수의 개수와 덧셈"
excerpt: "연습문제 lv1"

categories:
  - 프로그래머스
tags:
  - swift
  - 프로그래머스
  - 알고리즘
  - 코딩테스트
---
## 나의 풀이
```swift
func solution(_ left:Int, _ right:Int) -> Int {
    let arr = Array(left...right)
    var result:[Int] = []
    
    for number in arr {
        var count = 0
        for i in 1...number {
            
            if number % i == 0 {
                count += 1
            }
        }
        count % 2 == 0 ? result.append(number) : result.append(-number)
    }

    return result.reduce(0, +)
}
```
<img src="/assets/images/programmers/programmers02/01.png">
<br>
count 변수를 약수의 개수로 이용했다.
<br>
<br>

## 다른 사람 풀이
```swift
func solution(_ left: Int, _ right: Int) -> Int {
    return (left...right).map { i in (1...i).filter { i % $0 == 0 }.count % 2 == 0 ? i : -i }.reduce(0, +)
}
```
