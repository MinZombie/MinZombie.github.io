---
title: "[iOS] 테이블 뷰 Custom Header 사용하기"
excerpt: "커스텀 헤더, nib파일 사용하기"

categories:
  - ios
tags:
  - ios
  - custom header
  - UITableView
---

커스텀 헤더를 구현하는 방법은 두 가지가 있는데 첫번째는 UITableViewHeaderFooterView를 사용하는 방법이고 두번째는 서브클래싱을 이용하는 방법이다.

# UITableViewHeaderFooterView 사용해서 커스텀 헤더 만들기
***
```swift
tableView.register(UITableViewHeaderFooterView.self, forHeaderFooterViewReuseIdentifier: "customHeader")
```
우선 viewDidLoad에서 위와 같이 테이블뷰에 HeaderFooterView를 등록해야한다. 그리고 델리게이트를 통해서 커스텀을 해주면 된다.
```swift
extension ViewController: UITableViewDelegate {
    func tableView(_ tableView: UITableView, viewForHeaderInSection section: Int) -> UIView? {
        let header = tableView.dequeueReusableHeaderFooterView(withIdentifier: "customHeader")
        
        header?.textLabel?.text = list[section].title
        //header?.textLabel?.textAlignment = .center
        //header?.textLabel?.textColor = .systemBlue
        //header?.backgroundColor = .black
        
        return header
    }
```
Header/Footer도 재사용 매커니즘을 사용한다. 그래서 셀을 다루는 방법과 비슷하다.
이 메서드 안에는 텍스트만 설정을 한다고 한다. textAlignment 같은 경우는 여기서 설정을 하면 적용이 안되고 uiview를 파라미터로 받는 메서드에서 구현해야 한다. 밑에서 살펴보자.

<br>
```swift
func tableView(_ tableView: UITableView, willDisplayHeaderView view: UIView, forSection section: Int) {
        guard let header = view as? UITableViewHeaderFooterView else { return }
        
        let view: UIView = {
            let v = UIView(frame: .zero)
            v.backgroundColor = .brown
            
            return v
        }()
        
        header.textLabel?.textAlignment = .center
        header.textLabel?.textColor = .systemBlue
        header.backgroundView = view
        
    }
```
위에서 안된 textAlignment는 여기서 구현하면 잘 된다. 이 메서드 안에서는 시각적인 속성을 설정한다. 백그라운드 컬러 같은 경우는 헤더에 backgroundColor속성에 바로주면 적용이 안되고 오류 메시지가 뜬다. 이 경우에는 UIView 하나 생성하고 그 뷰에 BackgroundColor 값을 주고 헤더의 backgroundView에 새로 만든 UIView를 설정 해야한다.
<br>
<br>
<br>
<br>

# 서브클래스 이용해서 커스텀 헤더 만들기
***
<img src="/assets/images/ios/customSection/01.png">
<br>
<img src="/assets/images/ios/customSection/02.png">
<br>
View xib 파일을 만들어 주고 그 안에서 원하는 헤더를 만들어주고, 코코아 터치 클래스에서 UITableViewHeaderFooterView 클래스 파일을 만들고 그 안에 변수를 만들어서 xib 만든 것과 연결해서 사용하면 된다.  
<br>

>[TableView] Changing the background color of UITableViewHeaderFooterView is not supported. Use the background view configuration instead.

xib 파일을 만들자마자 제일 상위 뷰의 백그라운드 컬러를 default로 바꾸면 위의 메시지가 더 이상 나오지 않는다.

<br>
```swift
class CustomHeaderView: UITableViewHeaderFooterView {

    @IBOutlet weak var title: UILabel!
    
    override func awakeFromNib() {
        super.awakeFromNib()
        title.text = "123"
        title.layer.cornerRadius = 20
        title.clipToBounds = true
    }
}
```
awakeFromNib 메서드에는 초기화 코드를 구현해주면 된다.
<br>
```swift
 override func viewDidLoad() {
        let headerNib = UINib(nibName: "CustomHeader", bundle: nil)
        tableView.register(headerNib, forHeaderFooterViewReuseIdentifier: "customHeader")
    }

extension ViewController: UITableViewDelegate {
    func tableView(_ tableView: UITableView, viewForHeaderInSection section: Int) -> UIView? {
        let header = tableView.dequeueReusableHeaderFooterView(withIdentifier: "customHeader") as! CustomHeaderView

        header.title.text = list[section].title

        return header
    }

}
```
UINib파일을 테이블 뷰에 추가하고 델리게이트에서 우리가 만든 UITableViewHeaderFooterView를 다운캐스팅해서 가져와 사용한다. 코드를 작성하고 확인해봤는데 헤더의 높이가 이상하다면 스토리보드의 헤더부분 HeaderHeight 속성을 Automatic이나 원하는 높이를 설정하면 된다.
<br>
Custom Footer도 Custom Header와 만드는 방식이 똑같다.