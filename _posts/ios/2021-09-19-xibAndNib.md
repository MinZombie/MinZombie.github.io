---
title: "[iOS] xib과 nib 차이점"

categories:
  - ios
tags:
  - swift
  - xib
  - nib
---

- xib (Xml Interface Builder)하고 nib (NeXT Interface Builder)의 기능은 동일하나 xib는 xml 기반이고 nib은 바이너리 기반으로 이루어져있다.
- nib은 형상 관리 툴(Git 같은 것)하고 같이 사용할 때 문제가 있다. 그래서 xib로 대체해서 사용 중이다.
- xib는 컴파일시 nib으로 변환된다.