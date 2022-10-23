
---
title: "DerivedData에 있는 폴더 정리 후 SPM 라이브러리 못찾는 문제"

categories:
  - ios
tags:
  - ios
  - spm
---

아래와 같은 에러가 뜨면서 빌드가 안되는데

<img src ="https://user-images.githubusercontent.com/78908490/197396461-f950363b-b4dc-4cfb-b5ad-d66bca6187b7.png">

Xcode -> File -> Packages -> <span style="color: red">Resolve Package versions</span>을 누르면 해결이 된다
