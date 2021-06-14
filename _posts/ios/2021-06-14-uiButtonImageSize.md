---
title: "[iOS] UIButton 이미지 크기 크게 만드는 방법"
excerpt: "스토리보드 UIButton 이미지 사이즈 조절"

categories:
  - ios
tags:
  - ios
  - uibutton
---

버튼에 이미지를 넣고 크게 하고 싶어서 스케일을 라지로 해도 내가 원하는 만큼 커지지 않았다. Default Symbol Configuration의 Configuration에서 Point Size의 크기를 바꾸면 내가 원하는 크기로 바꿀 수 있다.
<br>
<img src="/assets/images/ios/uiButtonImageSize/01.png">
<br>
<img src="/assets/images/ios/uiButtonImageSize/02.png">
<br>
<img src="/assets/images/ios/uiButtonImageSize/03.png">
<br>
크기를 바꿀 때 주의해야 할 점은 버튼의 크기보다 더 큰 point size값을 주면 바뀌지 않는다. 그래서 버튼의 width와 height 값도 같이 바꿔야한다.