---
title: "[iOS] 코드로 뷰를 만드는 방법"
excerpt: "스토리보드 없이 코드로 뷰 만들기"

categories:
  - ios
tags:
  - ios
  - uiview
---


스토리보드를 통해서 뷰를 생성하는 것은 너무 쉬운데, 스토리보드만 사용해서 작업하지 않고 코드와 스토리보드 둘 다 사용하니까 코드를 통해서 UI를 생성하는 법을 공부해보려 한다.

View는 기본적으로 위치와 크기를 필요로 하는데 여기서 위치(CGPoint) + 크기(CGSize)는 Frame(CGRect)이다.  
**Frame은 슈퍼뷰의 지역좌표 내에서 뷰의 위치와 크기를 표현한다.**

### 코드
***
```swift
override func viewDidLoad() {
        super.viewDidLoad()

        let frame = CGRect(x: 100, y: 100, width: 100, height: 100)
        let v = UIView(frame: frame)

        v.backgroundColor = UIColor.systemGreen

        view.addSubview(v)

    }
```

위치와 크기를 지정하고 마지막으로 View(root view)에 내가 만든 View를 추가해준다.
