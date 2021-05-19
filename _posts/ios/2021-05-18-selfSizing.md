---
title: "[iOS] TableView 셀프 사이징 사용법"
excerpt: "테이블뷰 기본 셀 셀프사이징, 커스텀 셀 셀프사이징"

categories:
  - ios
tags:
  - ios
  - self sizing
  - UITableView
---

# 기본 셀에서 사용법
***
<img src="/assets/images/ios/selfSizing/01.png">
<br>
스토리보드에서 테이블뷰 옵션창을 보면 Row Height와 Estimate 항목에 Automatic이 체크되있으면 셀프사이징이 활성화 된것이다. 그리고 Label의 Line 값을 0으로 해주면 기본 셀에서 셀프사이징은 끝이다. 텍스트를 길게 입력 해보면 텍스트 길이에 따라 셀의 높이가 자동으로 늘어나는 것을 확인할 수 있다.  

만약 코드로 테이블뷰를 구현했다면 마찬가지로 코드로 Row Height, Estimate를 설정해주어야한다.
```swift
override func viewDidLoad() {
        tableView.rowHeight = UITableView.automaticDimension
        tableView.estimatedRowHeight = UITableView.automaticDimension
}
```
<br>
<br>
<br>

# 커스텀 셀에서 사용법
***
커스텀 셀에서 셀프사이징을 구성할 때에는 컨텐츠의 높이값 지정이 중요하다. 만약 안돼있다면 오류메세지와 함께 기본 셀 높이값으로 자동 설정된다.  

<img src="/assets/images/ios/selfSizing/02.png">
<br>
테이블 뷰 셀에 있는 Row Height 값은 프로토타입 셀에서 구성할 때 높이이다. 런타임에서는 우선순위가 낮고 Automatic이 활성화 되있으면 자동으로 계산해주고 아니면 테이블 뷰의 Row Height의 높이 혹은 델리게이트를 이용해서 설정한 높이로 표시가 된다.  
<br>
<br>
<br>

# 특정 셀 높이 고정 나머지는 셀프 사이징
위에서 살펴본 방법들은 모든 셀이 셀프사이징 이거나 모든 셀이 고정된 높이 값을 가지는 방법이다. 만약 반반 섞어서 하고 싶다면? 특정 셀의 높이는 설정하고 나머지 셀은 셀프 사이징으로 하는 방법으로는 델리게이트를 이용하는 것이다.
```swift
extension ViewController: UITableViewDelegate {
    func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
        if indexPath.row == 1 {
            return 200
        }

        return UITableView.automaticDimension
    }
}
```
<img src="/assets/images/ios/selfSizing/03.png">
<br>
그럼 1번 셀은 텍스트가 짧아도 200의 높이 값으로 설정이 됐다.
<br>
<br>
# <span style="color:red">셀프 사이징 주의사항</span>
***
컨텐츠가 모두 고정된 높이라면 셀프 사이징을 사용할 필요 없이 고정된 높이 값을 설정해주면 된다. 셀프 사이징을 이용하면 디바이스가 높이 값을 계산하기 때문에 고정된 높이 값보다 스크롤 성능이 느릴 수 있다.
