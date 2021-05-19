---
title: "[iOS] 테이블 뷰 Custom Cell 사용하기"
excerpt: "커스텀 셀 사용법, nib파일에 셀 만들기"

categories:
  - ios
tags:
  - ios
  - custom cell
  - UITableView
---
# 커스텀 셀
***
커스텀 셀을 사용하기 위해서는 UITableViewCell 클래스가 있는 새 파일이 필요하다.
<br>
<img src="/assets/images/ios/customCell/01.png">
<br>
<img src="/assets/images/ios/customCell/02.png">
<br>
```swift
class CustomTableViewCell: UITableViewCell {

    @IBOutlet weak var dateLabel: UILabel!
    @IBOutlet weak var cityLabel: UILabel!
    @IBOutlet weak var timeLabel: UILabel!
    
 
    
    override func awakeFromNib() {
        super.awakeFromNib()
        // Initialization code
    }

    override func setSelected(_ selected: Bool, animated: Bool) {
        super.setSelected(selected, animated: animated)

        // Configure the view for the selected state
    }

}
```
스토리보드 프로토타입 셀 안에 있는 컨텐츠들을 Outlet으로 연결할 때 방금 생성한 파일에 연걸해 줘야한다. 만약 ViewController에 연결을 하려고 하면 아래와 같이 오류가 나오는데 프로토타입 셀은 반복적으로 표시되는 템플릿으로 사용되기 떄문에 셀 안에 있는 Label을 접근할 때 몇번째 셀안에 있는 Label인지 알지 못해서 생기는 오류이다.
<br>
<img src="/assets/images/ios/customCell/03.png">
<br>
```swift
extension ViewController: UITableViewDataSource { 
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = timeTableView.dequeueReusableCell(withIdentifier: "customCell", for: indexPath) as! CustomTableViewCell
        
        cell.dateLabel.text = "오늘"
        cell.cityLabel.text = "베를린"
        cell.timeLabel.text = "22:00"
        
        return cell
    }
}
```
테이블 뷰의 셀에 접근할 때 프로토타입의 셀이 아닌 우리가 만든 셀의 클래스로 접근하려면 다운캐스팅으로 접근해야한다. 왜냐하면 dequeueResuableCell이 업캐스팅 되서 리턴되기 때문이다.
<br>
<br>
<br>
<br>
# 하나의 커스텀 셀을 여러 ViewController에서 사용하기
***
커스텀 셀 하나를 여러 뷰에서 사용하고 싶다고 똑같은 셀을 여러개 만들면 비효율적이다. 그래서 하나의 커스텀 셀을 여러곳에 사용하는 방법은 nib파일을 만들어서 거기에 커스텀 셀을 만드는 것이다. 스토리보드에서 만드는 방식하고 똑같다.
<br>
<img src="/assets/images/ios/customCell/04.png">
<br>
```swift
let customCell = UINib(nibName: "CustomCell", bundle: nil)
timeTableView.register(customCell, forCellReuseIdentifier: "customCell")
```
그리고 뷰컨트롤러 viewdidload에서 UINib을 활용해서 테이블뷰에 우리가 만든 커스텀 셀을 추가 하면된다. nib파일 안에서 셀의 identifier값을 줄 필요가 없는 이유는 여기서 identifier 값을 설정하기 때문이다.