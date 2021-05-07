---
title: "[Swift] 스위프트 truncatingRemainder란?"
excerpt: "Double 타입 나머지 구하기"

categories:
  - swift
tags:
  - swift
  - operator
---

스위프트에서 나머지 값을 구하려면 %(나머지 연산자)를 사용한다
```swift
9 % 4    // 1
-9 % 4   // -1
```
<span style="color:red">하지만</span> %는 Int끼리의 계산에만 적용이 가능하다. 그러면 소수점이 있는 Double, Float의 <span style="color:red">나머지</span>값을 구하려면?
##### truncatingRemainder(dividingBy:) 메서드를 사용한다.
<img src="/assets/images/truncatingRemainder/01.png">