---
title: "[iOS, Swift] NSAttributedString"
excerpt: "NSAttributedString, NSMutableAttributedString"

categories:
  - ios
tags:
  - ios
  - NSAttributedString
  - NSMutableAttributedString
---

### NSAttributedString을 간단하게 알아보자
NSAttributedString 객체는 문자열에 관련된 속성(폰트, 문자 사이의 간격 등등)을 이용할 때 필요하다.  
하나의 문자나 혹은 범위를 지정하여 여러 문자의 속성도 적용 가능하다. NSAttributedString은 읽기 전용이고, 수정이 가능한 NSMutableAttributedString도 있다. NSDictionary에 저장된 이름으로 문자열을 식별한다.
<br> 
쉽게 말해서 NSAttributedString은 텍스트의 일부분에 폰트를 바꾸고, 색상을 변경할 수 있다.
<br>
### 간단한 사용법

<img src="/assets/images/nsAttributedString/01.png">
<br>
속성값을 딕셔너리 형태로 키와 밸류를 설정하면 된다. 키에는 문자열의 원하는 속성을, 밸류에는 그 속성의 원하는 값을. 

그리고 NSMutableAttributedString을 활용해서 이미 지정된 속성값이라도 변경이 가능하다.
<img src="/assets/images/nsAttributedString/02.png">
<br>
### 참고하면 좋은 사이트
[Apple Developer](https://developer.apple.com/documentation/foundation/nsattributedstring)
[Attributed String Programming Guide](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/AttributedStrings/AttributedStrings.html#//apple_ref/doc/uid/10000036-BBCCGDBG)
[Hacking With Swift](https://www.hackingwithswift.com/articles/113/nsattributedstring-by-example)
***
<br>
NSAttributedString에 대해서 더 깊게 공부 하고 싶었는데 내용이 너무 어려웠다. 모르는 걸 다 찾다보니 양이 계속 늘어나서 일단은 지금 실력에서 모든 걸 알려고 하지 말고 어느정도만 받아들이고 익숙해 지는 것에 집중해야한다. 그리고나서 나중에 더 깊게 공부하면 된다.