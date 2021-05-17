---
title: "[iOS] UIDatePicker의 Count Down TImer모드 사용해보기"
excerpt: "카운트다운"

categories:
  - ios
tags:
  - ios
  - countDownTimer
  - UIDatePicker
---

UIDatePicker에서 카운트다운 모드를 사용할 수 있다. 하지만 Timer처럼 보일 뿐 시간이 자동으로 감소되지는 않는다. 결국 Timer.scheduledTimer를 사용해야 한다.
```swift
    var remainingTime = 0
    @IBOutlet weak var countdownLabel: UILabel!
    @IBOutlet weak var countdownPicker: UIDatePicker!
    
    @IBAction func startButton(_ sender: Any) {
        remainingTime = Int(countdownPicker.countDownDuration)
        
        Timer.scheduledTimer(withTimeInterval: 1, repeats: true) { timer in
            self.remainingTime -= 1
            self.countdownLabel.text = "\(self.remainingTime)"

            if self.remainingTime == 0 {
                timer.invalidate()
            }
        }
    }
    
    override func viewDidLoad() {
        countdownPicker.countDownDuration = 60
        
    }
```

UIDatePicker의 countDownDuration 속성은 카운트다운 할 시간을 설정한다. 초 단위를 입력해야 한다. 최소값은 1분, 최대값은 23시간 59분이다. 위에서 처럼 시간을 설정하면 DatePicker에서 다른 시간을 선택하더라도 위에서 설정한 시간이 실행된다.
그리고 countDownDuration 속성을 이용해서 사용자가 선택한 시간을 알 수 있고 시간은 Double로 표시된다
<br>
Timer.scheduledTimer를 사용해서 1초씩 감소하는 기능을 구현했다.
