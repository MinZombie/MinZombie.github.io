텍스트 필드는 alert 스타일에서만 가능
---
title: "[iOS] Alert안에 TextField 구현하기"
excerpt: "경고창에 텍스트 필드 추가, 텍스트필드 커스터마이징"

categories:
  - ios
tags:
  - ios
  - alert
  - text field
---

### 목표: TextField에서 텍스트를 입력받아 Label에 표시하기.
***

### 구현 순서
1. UIAlertController 만들기 (alert 스타일)
1. alert에 TextField 추가
1. 확인버튼 만들고 추가하기(확인버튼에서 TextField 텍스트를 Label에 표시하는 코드 구현)
1. Alert 표시
***

### 1. UIAlertController 만들기 (alert 스타일)
```swift
let controller = UIAlertController(title: nil, message: "Write something xD", preferredStyle: .alert)
```
<br>
### 2. alert에 TextField 추가
```swift
controller.addTextField { field in
            
        }
```
만약 텍스트필드를 2개 만들고 싶으면 addTextField를 두번 하면 된다.
<br>
### 3. 확인버튼 만들고 추가하기(확인버튼에서 TextField 텍스트를 Label에 표시하는 코드 구현)
```swift
let okAction = UIAlertAction(title: "Ok", style: .default) { action in
            if let firstTextField = controller.textFields?.first {
                self.firstLabel.text = firstTextField.text
            }
            if let secondField = controller.textFields?.last {
                self.secondLabel.text = secondField.text
            }
        }
```
텍스트필드를 2개 만들었기 때문에, 원하는 텍스트필드에 접근하기 위해서 first, last 속성을 사용했다.  
첫번째 텍스트필드는 첫번째 label에 표시를, 두번째 텍스트필드는 두번째 label에 표시하기 위해서..
<br>
### 4. Alert 표시
```swift
present(controller, animated: true, completion: nil)
```
<br>
그러면 다음과 같은 화면을 얻을 수 있다.
<br>
<img src="/assets/images/alertTextField/01.png">
<br>
### 결과
<img src="/assets/images/alertTextField/04.gif">  

***

### 커스터마이징
2번순서에서 addTextField 부분에서 커스터마이징이 가능하다
placeholder, 텍스트를 비밀번호입력창 처럼 가리기 등등..
커스터마이징을 통해서 로그인화면처럼 꾸밀 수 있으니 alert에 TextField로 구현하는 것도 괜찮을 것 같다.  
<span style="color:red">주의</span>해야 하는 점은 actionSheet에서는 TextField 구현이 안된다.
```swift
controller.addTextField { field in
            field.placeholder = "something!!"
            field.isSecureTextEntry = true
        }
```
- placeholder 속성은 TextField안에 텍스트 입력전에 옅은 회색으로 텍스트가 표시된다.    
- isSecureTExtEntry는 텍스트를 구별할 수 없게 *** 이런식으로 표시해준다.    

