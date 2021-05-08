---
title: "[iOS] Content Mode"
excerpt: "Content Mode의 종류와 기능"

categories:
  - ios
tags:
  - ios
  - content mode
---



####  Content Mode
***
* Content를 화면에 표시하는 것은 메모리와 씨피유가 많이 필요한 작업인데 View는 이벤트가 있을 때 마다 Content를 업데이트한다. 업데이트마다 Content를 다시 그리는 것은 비효율 적이라서 이를 해결 하기 위해서 Bitmap cache에 Content를 저장하고 똑같은 Content를 View에 그릴 때 재사용한다.

* **Bitmap cache 방식을 재사용 하는 방법은 Content Mode를 통해서 한다.**  
Content Mode에는 13가지가 있는데
  ##### 1. scaleToFill

  <img src="/assets/images/contentMode/scaleToFill.png" width="240" height="460">

  종횡비를 유지 하지 않고 뷰의 크기에 딱 맞게 조절해서 이미지가 찌그러져 보인다. 그래서 잘 사용하지 않는다.

  ##### 2. scaleAspectFit

  <img src="/assets/images/contentMode/aspectFit.png" width="240" height="460">

  종횡비를 유지하고 뷰의 크기에 맞추고, 만약 뷰의 종횡비와 이미지의 종횡비가 다를경우 위의 사진 처럼 뷰에 빈공간이 생긴다.

  ##### 3. scaleAspectFill

  <img src="/assets/images/contentMode/aspectFill.png" width="240" height="460">

  종횡비를 유지하고 뷰 전체를 빈공간 없이 채우다 보니 이미지의 크기가 뷰의 크기가 더 커서 짤릴 수 있다.

  ##### 4. redraw

  <img src="/assets/images/contentMode/redraw.png" width="240" height="460">

  이전과 다른게 없어 보이는데 이름에서도 알수 있듯이 setNeedsDisplay() 메서드를 통해서 다시 그리는 옵션이다.

  ##### 나머지 옵션들은 위치에 관한 것들이라 한번씩 보면 쉽게 파악할 수 있다.
