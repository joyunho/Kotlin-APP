---
layout: post
title: "Webhacking(AJAX)"
date: 2021-01-07 07:03:00 +0900
background: "/img/posts/05.jpg"
categories: ["development"]
---

AJAX
====
==> Asynchronouss JavaScript and XML <br>
HTML, 자바스크립트, JSON을 혼합하여 사용하는 기술을 의미
> JSON :: 웹서버와 데이터를 주고받을 떄 데이터를 표현하는 방법을 의미

![AJAX 검색에 사용하는 변수 + GET 메소드](https://user-images.githubusercontent.com/76092057/103825633-8b86bd80-50b8-11eb-883c-89087d315fcb.PNG){: width:"100%" height:"100%"}

소스코드 확인 결과
-----------------
1. 검색에 사용하는 변수는 title
2. GET 메소드를 사용함으로 URL에서도 변수와 변수에 대입한 값을 노출한다. 하지만, AJAX로 구현한 페이지이기 떄문에 URL에 있는 변수에 값을 입력하여도 결과를 출력하지 않는다.

* DB의 테이블 명을 확인하기 위해 UNION SELECT 구문을 사용한다.(이때, 쿼리의 칼럼 수가 기존 쿼리에서 호출하는 칼럼 수와 일치해야하는데, 이 경우, 칼럼의 수는 총 7개이다.)
  > 0' union select null, table_name, null, null, null, null, null from information_schema.tables#

![AJA SQL 인젝션 결과(테이블명)](https://user-images.githubusercontent.com/76092057/103826311-f258a680-50b9-11eb-9863-c18bfc3a74c3.PNG){: width:"100%" height:"100%"}

* 웹 애플리케이션에서 사용 중인 데이터베이스 bWAPP의 테이블 명을 찾기 위해서 SQL 인젝션 공격 시도
  > 0' union select null, table_name, null, null, null, null, null from information_schema.tables where table_schema="bWAPP"#

![AJAX bWAPP 테이블명 찾기](https://user-images.githubusercontent.com/76092057/103826571-6dba5800-50ba-11eb-8fc3-c70d356bfd3d.PNG){: width:"100%" height:"100%"}

* 5개의 테이블 중 users 테이블이 사용자의 계정 정보를 저장하는 테이블이라고 추정한 뒤, users 테이블 칼럼명을 출력하는 쿼리를 만든다.
  >  0' union select null, columns_name, null, null, null, null, null from information_schema.columns where table_name="users" and table_schema="bWAPP"#

![AJAX 계정 정보](https://user-images.githubusercontent.com/76092057/103826865-0d77e600-50bb-11eb-94e1-9e06d69ca522.PNG){: width:"100%" height:"100%"}

* 칼럼들의 내용을 확인할 수 있는 쿼리를 만든다
  > 0' union select null, id, login, password, admin, null, null from users#

![AJAX 공격 성공](https://user-images.githubusercontent.com/76092057/103827061-79f2e500-50bb-11eb-817f-79a30d7e8eaa.PNG){: width:"100%" height:"100%"}

* 결과 :: admin 칼럼은 관리자 계정의 순서 번호를 저장하므로 관리자 계정의 아이디는 "A.I.M" 이라는 것을 알 수 있다.

### 대응방안

![AJAX 대응방안](https://user-images.githubusercontent.com/76092057/103827316-0f8e7480-50bc-11eb-872e-9c4c4d12b833.PNG){: width:"100%" height:"100%"}

1. sqli_check_2 함수를 사용하여 입력한 SQL 구문을 쿼리로 인식하지 않게 우회하였음을 알 수 있다.
2. sqli_check_2 함수는 functions_external.php에 정의되어 있고 PHP 기본 제공 함수인 mysql_real_escape_string 함수를 사용하여 입력한 데이터를 우회한다.
3. mysql_real_escape_string 함수는 사용자 입력 값에 SQL 문법에서 사용하는 특수 문자가 있을 경우 백슬래시를 붙여 입력 데이터를 SQL 문법으로 인식하지 않게 방어한다.

***

Login Form/Hero
===============

* 아이디, 비밀번호란에 작음따옴표를 입력하여 SQL 인젝션 취약점이 있는지 확인한다.

![Logtin Form 데이터베이스 서버 파악](https://user-images.githubusercontent.com/76092057/103827713-f33f0780-50bc-11eb-9f24-f07bfccc8727.PNG){: width:"100%" height:"100%"}

* 항상 결과가 참인 쿼리를 아이디 입력란에서 삽입하고 확인
  > ' or 1=1#

![Login Form 항상 참인 쿼리](https://user-images.githubusercontent.com/76092057/103827857-3ac59380-50bd-11eb-8093-204f935a043b.PNG){: width:"100%" height:"100%"}
==> 결과 : 'neo'라는 사용자로 로그인에 성공하고 해당 사용자의 비밀번호 힌트도 출력된다.
<br>
(비밀번호를 입력하지 않아도 로그인이 되는 이유는 변수를 따로 입력받지 않고 AND 연산자를 사용하여 한 줄로 DB의 아이디와 비밀번호를 출력하기 때문에 발생하는 취약점이다.)

* 아이디를 알고 있고 있으면 항상 참인 쿼리를 만들어 neo 이외에 사용자로도 로그인이 가능하다.
  > alice ' or 'a'='a

![Login Form 공격 성공](https://user-images.githubusercontent.com/76092057/103828358-f4246900-50bd-11eb-80f3-5f1e6ab94fb5.PNG){: width:"100%" height:"100%"}

### 대응방안

![Login Form 대응방안](https://user-images.githubusercontent.com/76092057/103829197-2f269c80-50be-11eb-90c9-dc7b8fad9396.PNG){: width:"100%" height:"100%"}

1. 난이도 상에서는 작은따옴표를 입력하여도 오류메세지 출력 x, SQL 취약점이 없다.
2. sqli_check_2 함수를 사용하여 입력한 SQL 구문을 쿼리로 인식하지 않게 우회하였음을 알 수 있다.
3. sqli_check_2 함수는 functions_external.php에 정의되어 있고 PHP 기본 제공 함수인 mysql_real_escape_string 함수를 사용하여 입력한 데이터를 우회한다.
4. mysql_real_escape_string 함수는 사용자 입력 값에 SQL 문법에서 사용하는 특수 문자가 있을 경우 백슬래시를 붙여 입력 데이터를 SQL 문법으로 인식하지 않게 방어한다.

*** 

Blog
====
사용자가 입력한 내용을 저장하고 테이블 형태로 출력하는 페이지

* 텍스트 입력 공간에 작은따옴표를 입력하여 SQL 인젝션에 취약한지를 파악한다.

![stored blg SQL 취약점](https://user-images.githubusercontent.com/76092057/103831438-6cd7f500-50bf-11eb-9072-5d6c76a0679b.PNG){: width:"100%" height:"100%"}

* 오류 메세지를 살펴서 SQL 쿼리를 만들기 위하여 entry 변수에 다음과 같이 입력
  > '1

![stored blog SQL 쿼리](https://user-images.githubusercontent.com/76092057/103831732-0ef7dd00-50c0-11eb-83dd-3e4809084f32.PNG){: width:"100%" height:"100%"}

==> 작은따옴표의 짝이 맞지 않아서 발생하는 오류라는 것을 알 수 있다.

* 쿼리의 마지막에 사용자 아이디가 있으므로 작은따옴표와 괄호를 같이 사용하는 쿼리를 만든다.
  > I like honey',(select password from bWAPP.users where id=1 limit 0,1)#

![stored blog 공격 성공](https://user-images.githubusercontent.com/76092057/103831956-93e2f680-50c0-11eb-8305-41cd259873e0.PNG)
{: width:"100%" height:"100%"}


### 대응방안

![stored blog 대응방안](https://user-images.githubusercontent.com/76092057/103832075-d4db0b00-50c0-11eb-9f09-5cb6d54805b1.PNG){: width:"100%" height:"100%"}

1. sqli_check_2 함수를 사용하여 입력한 SQL 구문을 쿼리로 인식하지 않게 우회하였음을 알 수 있다.
2. sqli_check_2 함수는 functions_external.php에 정의되어 있고 PHP 기본 제공 함수인 mysql_real_escape_string 함수를 사용하여 입력한 데이터를 우회한다.
3. mysql_real_escape_string 함수는 사용자 입력 값에 SQL 문법에서 사용하는 특수 문자가 있을 경우 백슬래시를 붙여 입력 데이터를 SQL 문법으로 인식하지 않게 방어한다.



 