---
layout: post
title: "Webhacking(Blind SQL Injection)"
date: 2021-01-15 14:34:00 +0900
background: "/img/posts/05.jpg"
categories: ["development"]
---

Blind SQL Injection
===================
==> 쿼리의 결과를 참과 거짓으로만 출력하는 페이지에서 사용하는 공격이다.

* substr
  ==> 첫 번째 인자로 받은 문자열을 지정한 길이만큼 출력하는데, 주로 문자하나씩 추력하여 이름을 알아내는데 사용한다.
* ascii
  ==> 문자를 아스키코드로 변환하는데, 작음따옴표(')를 우회하는 변수일 때 문자를 입력하기 위하여 사용한다.
* limit
  ==> 문자열의 길이를 반환한다. 문자열 길이를 알아내면 substr 함수로 문자열 추측하기 쉬워진다. 

### Boolean Based

==> 참과 거짓만 출력하는 페이지에 공격자가 조작한 쿼리로 인해 데이터베이스 내용을 노출하는 취약점이다. 쿼리는 데이터베이스 내용이 일치하여 웹페이지에서 참을 출력할 떄까지 임의의 값을 대입한다.

![Boolean Based(문법 오류)](https://user-images.githubusercontent.com/76092057/104687857-56770c80-5743-11eb-82c8-8fae2e4b3209.PNG)
{: width:"100%" height:"100%"}

* 문법 오류 메세지를 확인 ==> SQL 인젝션 공격이 가능하다.

![Boolean Based(항상 참이 되는 쿼리)](https://user-images.githubusercontent.com/76092057/104688417-0cdaf180-5744-11eb-9928-713c53f2122c.PNG){: width:"100%" height:"100%"}

> ' or 1=1#

* 해당 영화가 존재한다는 메세지를 출력 ==> 결과가 참일 때 출력하는 메세지, 이를 통해 Boolean Based SQL 인젝션이 가능하다.

![Boolean Based(항상 거짓이 되는 쿼리)](https://user-images.githubusercontent.com/76092057/104688820-c4700380-5744-11eb-8bd7-d0c3f73fb185.PNG){: width:"100%" height:"100%"}

> ' or 1=2#

* 해당 영화가 존재하지 않는다는 메세지를 출력 ==> 위에 두 메세지를 통해 쿼리의 참과 거짓을 판별할 수 있다는 것을 확인

![Boolean Based(UNION SELECT 공격)](https://user-images.githubusercontent.com/76092057/104689461-e4ec8d80-5745-11eb-835b-f6f6a2f95570.PNG){: width:"100%" height:"100%"}

> ' UNION SELECT ALL 1,2,3,4,5,6,7#

* 검색한 영화가 데이터베이스에 있는지만 체크하기 때문에 쿼리의 결과를 출력하지는 않는다.

