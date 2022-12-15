---
title: "[Swift] CustomStringConvertible"

categories:
  - swift
tags:
  - swift
  - CustomStringConvertible
---

# CustomStringConvertible란?
프로토콜의 한 종류로, 인스턴스를 문자열로 커스텀할 때 사용을 한다. 특히 로그를 찍어볼 때 아주 유용하다.
<br></br>
# 사용법
```
struct Person {
    let name: String
    let age: Int
}

let god = Person(name: "messi", age: 99)
print(god)

// 결과
// Person(name: "messi", age: 99)
```
<br></br>
```
extension Person: CustomStringConvertible {
    var description: String {
        return "이름은 \(name), 나이는 \(age)살 입니다"
    }
}
// 결과
// 이름은 messi, 나이는 99살 입니다
```

CustomStringConvertible 프로토콜을 채택하게 되면 description이라는 변수를 정의 해줘야한다. 여기에 정의한 문자열이 인스턴스를 표현할 때 나오게된다.
<br></br>
<br></br>
애플 공식문서에 보면 설명이 잘 나와있고 어렵지 않은 개념이라 쉽게 이해가 가능했다.