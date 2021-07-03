---
title: "[iOS] 싱글톤(Singleton) 디자인패턴"
excerpt: "싱글톤 구현, 장단점"

categories:
  - ios
tags:
  - ios
  - singleton
---

# Singleton이란?
***
여러곳에서 싱글톤패턴을 따르는 클래스를 호출해도 똑같은 객체가 호출된다. 즉 하나의 객체가 처음에 생성 되고 다음에 호출 됐을 때도 앞에서 생성된 객체가 호출된다. 그래서 고정된 메모리값을 가지고 있어서 효율적이다. 앱 내에서 딱 하나만 있기 때문에 다른 클래스에 공유해서 사용이 가능하다.
<br>
<br>

# 구현 방법
***
```swift
class User {
    static let shared = User()

    name: String
    age: String

    private init () {}
}

var user = User.shared
user.name = "aa"
```
static을 이용해서 프로퍼티를 만들고, 나중에 이 프로퍼티를 통해서 접근이 가능하다. static을 사용해서 인스턴스를 생성하게 되면 사용시점에 초기화가 돼서 첫 인스턴스를 생성하기 전까지는 메모리에 올라가지 않는다(lazy처럼).
<br>
init을 private으로 설정한 이유는 다른곳에서 인스턴스 생성을 막기 위해서다.
<br>
<br>

# 언제 사용?
***
- DBCP(DataBase Connection Pool)처럼 공통된 객체를 여러개 생성해서 사용할 때(쓰레드풀, 캐시, 대화상자, 사용자 설정, 레지스트리 설정, 로그 기록) 싱글톤 클래스로 쉽게 접근하고 싶을 때
- 하나의 객체임을 보장하고 싶을 때
- 다른 클래스들과 쉽게 공유하고 싶을 때