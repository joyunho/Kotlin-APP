---
layout: post
title: "Webhacking(iframe)"
date: 2020-12-24 11:24:00 +0900
background: "/img/posts/04.jpg"
categories: ["development"]
---

# Iframe 인젝션

ifram은 HTML 문서 안에서 또 다른 HTML 문서를 출력하는 태그,
어느 위치든 상관없이 인젝션 공격이 가능하다. iframe 인젝션은
독립적으로 만들 수 있어서 hTMl 인젝션 중 에서도 공격에 자주
사용한다.

#iframei.php 페이지는 Get 방식으로 데이터 전송 받음
==> URL에 변수 노출<br>

|  ParamURL   | ParamWidth  | ParamHeight |
| :---------: | :---------: | :---------: |
| 연결할 주소 | 출력할 크기 | 출력할 크기 |


![iframe rebots](https://user-images.githubusercontent.com/76092057/103058414-6dfc2300-45e5-11eb-9386-0c0d39197003.PNG)
==> ParamUrl 변수의 값 == rebot.txt
(이 변수에 입력한 내용이 iframe 태그에 추가)

![iframe 공격용 HTML](https://user-images.githubusercontent.com/76092057/103058468-94ba5980-45e5-11eb-89e9-652abd6f1709.PNG)
==> iframe 태그로 사용자 모르게 악의적인 HTML페이지를 출력하는
공격을 하기 위해 HTML 페이지 작성

![iframe 기존 URl](https://user-images.githubusercontent.com/76092057/103058537-c4696180-45e5-11eb-832e-cc0e97874c05.PNG)
==> 기존 URL에 bad.htm페이지를 iframe의 src속성에 입력
- "htt(t)p://192.168.56.104/bWAPP/iframei.php?ParamUrl=robots.txt">   
  </iframe><iframe src="bad.html" width="250" height="250"></iframe>
  &ParamWidth=250&ParamHeight=250"