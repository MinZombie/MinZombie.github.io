---
title: "[iOS] UITableView의 Separator에 대해서"
excerpt: "Separator 스타일,컬러,인셋"

categories:
  - ios
tags:
  - ios
  - table view
  - separator
---

##### Separator는 셀과 셀 사이에 있는 선을 말하고, 셀을 시각적으로 구분하기 위한 것이다.
### <span style="color:red">separator style</span>  
<img src="/assets/images/separator/01.png">
<br>

- none: 선을 표지하지 않거나 커스텀 separator를 위해 사용
- default, single line: 선을 하나만 표시
- single line etched: 지금은 더 이상 사용하지 않는다.

### <span style="color:red">separator color</span>
<img src="/assets/images/separator/02.png">
<br>
style 속성 밑에서 색상을 고를 수 있다.
그럼 전체 separator에 적용이 되고, 셀마다 다른 separator 색상을 원하면 커스텀으로 구현해야한다.

### <span style="color:red">separator inset</span>
<img src="/assets/images/separator/03.png">
<br>
<img src="/assets/images/separator/04.png">
<br>
separator inset은 separator의 여백을 말한다.
속성에는 Automatic, Custom이 있다  

- Automatic: 기본 설정값으로 왼쪽에 15포인트 있다.
- Custom: 원하는 값을 왼쪽이나 오른쪽에서 설정할 수 있다.
    - From Cell Edges: 양 끝에서 부터 여백을 주는 방식
    - From Automatic Insets: 사용환경에 따라 알아서 설정해주는 방식, 다른부분과 겹치는 것을 방지할 떄 주로 사용
<br>
##### 그리고 프로토타입 셀에 inset값을 직접설정 가능하다.
<br>
### 코드
***
공통적으로 구현하고 싶을때 이런식으로 구현하면 된다. 만약 각 cell마다 다른 설정을 하고 싶다면, table view cell의 indexPath를 활용하면 된다.
```swift
    tableView.separatorStyle = .singleLine
    tableView.separatorInset = UIEdgeInsets(top: 0, left: 0, bottom: 0, right: 0)
    tableView.separatorInsetReference = .fromAutomaticInsets
    tableView.separatorColor = .blue
```
separatorInset에 top, bottom값은 적용되지 않는다.
<br>

```swift
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        
    }
```
위의 함수에 cell마다 다른 설정을 하는데, 주의해야 할 점은 재사용 큐를 사용하기 때문에 다른 cell에도 적용이 된다.그래서 내가 원하지 않는 cell에는 table view separator의 기본값을 꼭 설정해야 한다.