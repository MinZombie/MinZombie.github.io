---
title: "[iOS] 커스텀 디코딩 하기"
excerpt: "원하는 디코딩 로직 만들기"

categories:
  - ios
tags:
  - ios
  - JSON
  - decode
---
참고한 사이트: [애플 문서](https://developer.apple.com/documentation/foundation/archives_and_serialization/encoding_and_decoding_custom_types)
<br>
expanded cell(셀을 탭하면 크기가 늘어나고 줄어드는 기능)을 구현하는데 셀마다 지금 셀이 늘어난 상태인지 아닌지 하는 값이 필요했고 json을 디코딩해서 데이터를 사용하고 있는데 json에는 위에서 말한 상태값이 없었다. 쉽게 말해서 내가 구현한 구조체하고 json의 데이터 구조하고 달랐다. 그래서 원하는 디코딩 로직을 직접 추가해서 해결해봤다.

```swift
// JSON
{
    "title" : "",
    "year": "",
    "poster" : ""
},

// 구조체
struct Film: Codable {
    var title: String
    var year: String
    var poster: String
    var isExpanded: Bool
}    
```
```swift
init(from decoder: Decoder) throws {
      let container = try decoder.container(keyedBy: CodingKeys.self)
      title = try container.decode(String.self, forKey: .title)
      year = try container.decode(String.self, forKey: .year)
      poster = try container.decode(String.self, forKey: .poster)
      isExpanded = false
}
```
