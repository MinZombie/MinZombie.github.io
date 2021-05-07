---
title: "[iOS] Unwind Segue 란?"
excerpt: "Unwind Segue 연결, 구현 방법, 실행 제어"

categories:
  - ios
tags:
  - ios
  - segue
  - unwind
---
# Unwind Segue
***
Segue는 source화면에서 destination화면으로 이동할 때 사용하는데, 그 반대의 경우 destination -> source는 불가능하다. 이 때 사용하는 것이 unwind segue다.
예를 들어서 3개의 뷰가 있고 우리는 3번뷰에 있다. 3번뷰는 1번,2번뷰를 통해서 왔고 unwind segue를 통해서 1번뷰 혹은 2번뷰로 돌아갈 수 있다.

### 메서드
***
- func <span style="color:red">shouldPerformSegue</span>(withIdentifier: String, sender: Any?) -> Bool  
unwind segue와 연결된 액션을 실행할 수 있는 뷰 컨트롤러를 검색하고 실행 여부를 결정한다. 만약 2개의 뷰 컨트롤러에 2개의 액션이 있을경우 identifier값으로 구별해서 처리한다.
- func <span style="color:red">prepare</span>(for: UIStoryboardSegue, sender: Any?)  
화면 전환 전 실행되는 메서드로 뷰 컨트롤러에게 segue가 실행 될 것이라고 알려준다.
- func <span style="color:red">canPerformUnwindSegueAction</span>(Selector, from: UIViewController, sender: Any?) -> Bool  
segue와 연결된 액션을 실행할 수 있는지 확인한다.


<br>
### 구현 방법
<img src="/assets/images/unwind1.png">
일단 3개의 뷰가 있고 1번뷰에서 버튼을 누르면 2번뷰로 2번뷰에서 버튼을 누르면 3번뷰 이동하고 3번뷰에서 1번뷰 혹은 2번뷰로 돌아가는 기능을 구현하려 한다.

일단 첫번째로 1번뷰로 가기 위해서 3번뷰의 1번뷰로 가기위한 빨간 버튼을 unwind로 연결해야 하는데 방법은  
```swift
@IBAction func unwindToFirst(_ unwindSegue: UIStoryboardSegue) {
        
    }
override func viewDidLoad() {
        
    }
```
가고 싶은 뷰 컨트롤러에서 액션을 위와 같이 구현한다. 그리고
<img src="/assets/images/unwind2.png">
빨간색 버튼에서 컨트롤키를 누르고 마우스 클릭 후 사진에 있는 3번째 아이콘에 가면 된다. 그러면 방금 구현한 Action의 이름(unwindToFirst)이 나오면 연결해 준다.

그 외에 unwind segue를 제어나 처리하는 패턴을 사용하고 싶을 땐 위에서 소개한 메서드를 사용하면된다.
##### shouldPerformSegue, prepare 메서드는 destination 화면에서
```swift
override func shouldPerformSegue(withIdentifier identifier: String, sender: Any?) -> Bool {
        
        return true
    }
    
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        
    }
```
##### canPerformUnwindSegueAction 메서드는 source 화면에서
```swift
override func canPerformUnwindSegueAction(_ action: Selector, from fromViewController: UIViewController, sender: Any?) -> Bool {
        
        return true
    }
```

#### 작동 순서
***
shouldPerformSegue호출이 되고 뷰 컨트롤러를 찾고 true를 반환하면 -> canPerformUnwindSegueAction호출 true 반환하면 -> prepare 호출 -> unwind와 연결된 action 호출 -> 화면 이동

#### 결과
***
<img src="/assets/images/unwind3.gif">