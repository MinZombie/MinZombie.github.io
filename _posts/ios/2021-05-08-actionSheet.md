---
title: "[iOS] actionSheet 사용해서 경고창 표시하기"
excerpt: "actionSheet 사용 방법, 아이패드 사용시 주의점"

categories:
  - ios
tags:
  - ios
  - alert
  - swift
---

주로 표시 할 버튼이 3개 이상일 때 actionSheet를 사용한다.

### 사용 방법
actionSheet도 사용 방법은 alert와 같은데, UIAlertController의 세번째 파라미터를 actionSheet로 지정하기만 하면 된다.
***

### alert와 actionSheet의 차이점
- 표시방식: alert는 가운데서 표시되고, actionSheet는 밑에서 표시된다.
- 그리고 actionSheet에서 cancel스타일로 지정된 액션은 맨 아래에 표시된다.
<img src="/assets/images/actionSheet/01.png">
<br>
***

### actionSheet 사용시 주의점
만약 actionSheet를 <span style="color:red">아이패드</span>에서 사용 할 떄 컴파일 에러가 있을 수 있다. 그 이유는 아이패드에서는 popover형태로 사용해서 위치와 크기를 지정해야 하기 때문이다.
아이폰에서의 actionSheet의 표시방식과 아이패드에서의 표시방식은 다르다.  
표시되는 위치가 다르고 cancel버튼의 유무도 차이가 있다.
<img src="/assets/images/actionSheet/02.png">
<br>
```swift
@IBAction func alertButton(_ sender: UIButton) {
    let controller = UIAlertController(title: "Alert title", message: "This is a message", preferredStyle: .actionSheet)

    if let popoverController = controller.popoverPresentationController {
            popoverController.sourceView = view
            popoverController.sourceRect = sender.frame
        }

    present(controller, animated: true, completion: nil)    
}    
```
만약 <span style="color:red">일반적인 버튼</span>에 팝오버를 사용하기 위해서는 popoverPresentationController 속성을 사용한다. 그리고 밑에 두가지 속성을 지정해 줘야한다.
- sourceView:UIView? 팝오버를 표시하는 컨테이너(크기) 속성
- sourceRect: CGRect 사각형의 팝오버를 어디에 표시할지 정하는 속성  
<br>

<span style="color:red">bar 버튼</span>에 사용하고 싶다면
- barButtonItem: UIBarButtonItem? 속성에 바 버튼 아이템을 설정해주면 된다.