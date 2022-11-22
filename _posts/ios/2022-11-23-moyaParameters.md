---
title: "Moya 라이브러리에서 하나의 key와 여러 value로 파라미터를 url에 넣을 때 생기는 문제 해결 방법"

categories:
  - ios
tags:
  - ios
  - moya
---

<span style="color:red">name="first"&name="second"&name="third"</span> 의 url을 기대하고 아래와 같이 작성을 했는데
<img src="https://user-images.githubusercontent.com/78908490/203363327-7a335f43-e72d-4e7c-8057-22a553a8440f.png">
결과는 아래 처럼 %5B%5D 값이 들어가서 api 호출이 제대로 되지 않는다.
<span style="color: red">name%5B%5D=first&name%5B%5D=second&name%5B%5D=third</span>

알아보니 똑같은 key에 여러 value를 적용하려고 배열을 사용할 때 [] 대괄호까지 인식을 해버려서 생긴 문제였다.

alamofire github을 참고해서 해결 방법을 찾았는데, 아래 스샷처럼 작성했더니 더 이상 대괄호를 인식하지 않고 <span style="color: red">name=first&name=second&name=third</span> 처럼 원하는 주소가 나왔다.
<img src="https://user-images.githubusercontent.com/78908490/203365647-4efcbf76-d176-48f7-9de4-f0743ecdfa0b.png">

URLEncoding할 때 대괄호를 포함하는게 default여서 noBrackets 옵션으로 바꿔야한다
