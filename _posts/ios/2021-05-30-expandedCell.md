---
title: "[iOS] TableView의 크기가 늘어나는 cell 만들기"
excerpt: "셀 누르면 크기가 변하는 기능"

categories:
  - ios
tags:
  - ios
  - expanded cell
  - self sizing
---
더보기 버튼 같은 것들을 누르면 새로운 정보가 셀을 밑으로 늘리면서 보여주는 기능이다. 쉽게 말해서 <span style="color:red">셀이 확장</span>이 되는 것이다. expanded cell 이라는 키워드로 찾아보면 된다.
<br>
이 글에서 만들어 볼 것은 셀을 탭하면 많은 양의 텍스트를 보여주는 것이다.
<br>
우선 더미데이터를 만들기 위해서 Data라는 구조체에 text 변수와 셀이 지금 늘어났는지 안늘어났는지 상태값을 저장하기 위한 isExpanded 변수를 만들었다.
```swift
struct Data {
    var text: String
    var isExpanded: Bool
}
```
<br>
```swift
extension ViewController: UITableViewDataSource {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return list.count
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath)
        let target = list[indexPath.row]
        
        cell.textLabel?.text = target.isExpanded ? target.text : "Read more"
        
        return cell
    }
}

extension ViewController: UITableViewDelegate {
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        guard let cell = tableView.cellForRow(at: indexPath) else { return }
        var target = list[indexPath.row]
        
        // 1.
        target.isExpanded = !target.isExpanded
        list[indexPath.row] = target
        
        cell.textLabel?.text = target.isExpanded ? target.text : "Read more"
        
        // 2.
        tableView.beginUpdates()
        tableView.endUpdates()
        
    }
}
```
셀을 탭하면 ui가 변하기 때문에 UITableViewDelegate 프로토콜을 채택하고 몇번째 셀이 탭이 되었는지 알아야 하기 때문에 cellForRow 메서드를 사용한다.
1. 셀을 탭하면 isExpanded 값이 토글이 된다(true <-> false). 그리고 list 배열에 바뀐 값을 저장한다. 이렇게 하는 이유는 구조체(위에서 만든 Data라는 구조체)를 사용하기 때문이다. 구조체는 인스턴스를 복사하기 때문에 target의 값을 바꿔도 list의 값은 바뀌지 않는다.

2. tableView의 insert, reload, delete, selection 등의 작업을 애니메이션과 함께 처리할 수 있다. 셀이 탭이 되면 셀을 리로드 해줘야 ui가 업데이트 되면서 모든 데이터가 표시가 된다.
<br>
<br>
<img src="/assets/images/ios/expandedCell/01.gif" width=480>