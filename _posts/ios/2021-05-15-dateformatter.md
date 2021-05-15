---
title: "[iOS] DateFormatter로 원하는 날짜형식으로 바꾸기"
excerpt: "날짜 형식 바꾸기, 상대적인 날짜 형식, 지역화 된 날짜 형식"

categories:
  - ios
tags:
  - ios
  - DateFormatter
---

# 1. DateFormatter 인스턴스 만들기
```swift
let date = DateFormatter()
```
<br>
# 2. 스타일 지정(기본 스타일 or 커스텀)
```swift
// 기본스타일
date.dateStyle = .full
date.timeStyle = .full

// 커스텀
date.dateFormat = "MM/dd/yyyy"
```
dateStyle, timeStyle에는 full뿐만 아니라 short, medium, long, none가 있다. 두 스타일 중 하나는 꼭 설정해야한다. 만약 둘 다 none을 설정하면 값이 표시되지 않는다.
커스텀 형식으로 사용할 때 https://nsdateformatter.com/ 사이트를 참고하면 좋다.
<br>

# 3. 날짜를 스트링으로 변환
```swift
date.string(from: Date())
```
만약 옵셔널 Date를 사용하면 string(to: Date)로 언래핑 없이 스트링으로 변환이 가능하다. 그냥 Date를 사용하면 위의 string(from: Date)를 사용하면 된다.
<br>
***
<br>
# 지역화에 따른 날짜 형식 사용하기
setLocalizedDateFormatFromTemplate 메서드로 그 지역의 날짜 형식으로 변경 할 수 있다.
```swift
date.setLocalizedDateFormatFromTemplate("MMM yyyy")
date.locale = Locale(identifier: "ko_KR")
date.string(from: Date())
```
지역화된 날짜를 표현하고 싶다면 당연히 지역을 설정해 줘야한다. 그리고 만약 두 지역의 형식을 사용하고 싶다고 해서 처음에 형식을 한번만 지정하고 locale 속성값만 두 번을 준다고 제대로 지역화 된 날짜가 나오지 않는다.
처음에 지역을 설정하고 다음에 날짜 형식을 지정해야 한다. 두 곳을 원한다면 (지역설정 - 날짜 형식 설정)을 두 번 해야 한다. setLocalizedDateFormatFromTemplate 메서드가 지역에 맞게 업데이트 자동으로 되지 않기 때문에.
```swift
date.locale = Locale(identifier: "ko_KR")
date.setLocalizedDateFormatFromTemplate("MMM yyyy")
date.string(from: Date())

date.locale = Locale(identifier: "en_US")
date.setLocalizedDateFormatFromTemplate("MMM yyyy")
date.string(from: Date())
```
위의 결과 값은 2021년 5월  
아래는 May 2021
<br>
***
<br>
# 상대적인 날짜 표시하기
doesRelativeDateFormatting 변수를 true로 설정하면 최대 48시간 내 날짜를 상대적으로 표시가 가능하다.
한마디로 오늘, 내일, 어제와 같은 값을 얻을 수 있다.
```swift
let today = Date()
let tomorrow = today.addingTimeInterval(3600 * 24)
let yesterday = today.addingTimeInterval(3600 * -24)

let date = DateFormatter()

date.locale = Locale(identifier: "ko_KR")
date.dateStyle = .full
date.doesRelativeDateFormatting = true

print(date.string(from: today))
print(date.string(from: tomorrow))
print(date.string(from: yesterday))

// 오늘
// 내일
// 어제
```
addingTimeInterval은 매초 더해지기 때문에 3600초로 1시간을 설정하고 하루인 24시간을 곱했다.