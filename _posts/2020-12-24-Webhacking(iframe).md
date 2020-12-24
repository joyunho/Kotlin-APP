---
layout: post
title: "Webhacking(iframe)"
date: 2020-12-24 11:24:00 +0900
background: "/img/posts/04.jpg"
categories: ["development"]
---

Iframe 인젝션
============

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
- "http://192.168.56.104/bWAPP/iframei.php?ParamUrl=robots.txt">   
  </iframe><iframe src="bad.html" width="250" height="250"></iframe>
  &ParamWidth=250&ParamHeight=250"

![iframe 공격 성공(low)](https://user-images.githubusercontent.com/76092057/103058882-be27b500-45e6-11eb-980f-249c14e9c859.PNG)

==> 공격 성공

# 사용자 몰래 iframe 인젝션 공격을 하는 방법
iframe의 'width' 속성과 'height'속성을 0으로 수정한다.
(이떄, 높이와 넓이가 같이 출력된다면 페이지가 이상하다는 점을 
발견 할 수 있지만 이상한 점을 눈치 못채도록 높이 속성 값을
아주 큰값으로 설정하면 된다.)

대응 방안
--------
![iframe 대응방식](https://user-images.githubusercontent.com/76092057/103059292-0693a280-45e8-11eb-94e4-a19c1896e955.PNG)   

==>xss_check_3함수로 입력 데이터를 우회한다.<br>
즉, iframe인젝션을 막기 위해서는 htmlspecialchars 함수를   
사용하여 웹브라우저에서 iframe 태그에 사용되는 문자들을   
HTML 태그로 해석 하지 않게 입력 데이터를 UTF-8로 인코딩한다.

OS 커맨드 인젝션
===============
취약한 변수로 시스템 명령어를 주입하여 서버 운영체제에 접근하는 공격   
보통 웹 페이지에서 서버의 시스템 셸을 호출할 떄 관리자가 의도한 명령어
가 아닌 다른 명령어를 주입하여 서버 정보를 알아낸다.
<br>
==> 파이프라인은 둘 이상의 명령어를 실행할 때 사용하며 앞의 명령어를
실행한 후 파이프라인 뒤에 있는 명령어를 실행한다.

![파이프 라인을 이용한 os 커맨드 인젝션 공격](https://user-images.githubusercontent.com/76092057/103061335-6725de00-45ee-11eb-8126-a44ae3f4a22c.PNG)

==> 공격 성공
# Netcat 실습 실패(추후 추가 예정)

대응방안
-------
![os 커맨드 인젝션 대응방안](https://user-images.githubusercontent.com/76092057/103061561-12369780-45ef-11eb-94d6-52ac564ccc1a.PNG)

==> 시스템 명령어를 외부에서 사용하지 못하도록 하는게 가장 좋지만, 
부득이하게 시스템 명령어를 사용하여야 할 경우에는 필요한 명령어
이외에 다른 명령어를 사용할 수 없도록 '&, ;, |" 문자를 우회한다.

PHP 코드 인젝션
==============
PHP에서 exec() 함수나 eval() 함수를 사용한 경우 세미콜론(;)
을 사용하여 다른 함수를 실행한다는 취약점이 있다.   
취약점이 있는지 파악하려면 세미 콜론과 system함수를 사용한다.

![PHP 인젝션 whoami 명령어](https://user-images.githubusercontent.com/76092057/103061195-e2d35b00-45ed-11eb-8a5b-df356041277a.PNG)
==> 다른 명령어를 사용하여 공격 
(but, 상위 권한의 사용자만 접근할 수 있는 파일인 경우에는 
결과를 출력하지않는다.)

# Netcat 실습 실패(추후 추가 예정)

대응방안
-------
![PHP 인젝션 대응 방안](https://user-images.githubusercontent.com/76092057/103061932-0f887200-45f0-11eb-916d-e41f1b33534f.PNG)
==> htmlspecialchars 함수는 두 번쨰 인자에 'ENT _QUOTES'를 
추가하여 크로스 사이트 스크립팅에 사용되는 특수 문자들을
HTML 엔티티 코드로 변환한다.

SSI 인젝션
=========
SSI는 HTML 페이지의 전체 코드를 수정하지 않고 공통 모듈 파일로
관리하며 동적인 내용을 추가하기 위하여 만들어진 기능이다.
SSI를 사용하는 웹 페이지의 경우 SSI지시어를 처리하기 위한
'.shtml' 확장자 파일을 생성한다.

![SSI 기능 확인](https://user-images.githubusercontent.com/76092057/103062141-b53be100-45f0-11eb-8eea-25b37529f6f2.PNG)
==> 'ssii.shtml'페이지를 호출하는데, 이 페이지로 웹페이지에서
SSI 기능을 사용한다는 사실을 파악 가능

![ssi 명령어 실행 결과](https://user-images.githubusercontent.com/76092057/103062481-9f7aeb80-45f1-11eb-89ae-2810a1210ea0.PNG)
==> <!--#echo var="DATE_LOCAL" --> 명령어 입력 결과

![ssi 공격 성공 2](https://user-images.githubusercontent.com/76092057/103062570-ee288580-45f1-11eb-93c3-2d4e745896a2.PNG)
==> <!--#exec cmd="cat /etc/passwd" --> 명령어 입력 결과

# Netcat 실습 실패(추후 추가 예정)

대응방안
-------
![ssi 대응방안](https://user-images.githubusercontent.com/76092057/103062767-99d1d580-45f2-11eb-8c4a-1d1c9d53ba91.PNG)
==> htmlspecialchars함수는 두 번째 인자에 "ENT_QUOTES'를 추가
하였는데, XSS에 사용되는 특수 문자들을 HTML 엔티티 코드로 변환한
후 입력하여도 웹브라우저에서는 문자로 인식한다.
