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

![ParamUrl](C:\Users\whdbs\OneDrive\바탕 화면\WEB HACKING\사진\iframe rebots.png)
==> ParamUrl 변수의 값 == rebot.txt
(이 변수에 입력한 내용이 iframe 태그에 추가)
