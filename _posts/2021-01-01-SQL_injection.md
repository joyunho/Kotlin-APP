---
layout: post
title: "Webhacking(SQL_Injection)"
date: 2021-01-01 09:44:00 +0900
background: "/img/posts/03.jpg"
categories: ["development"]
---

SQL_Injection
=============

SQL 인젝션은 사용자가 입력한 값을 서버에서 검증하지 않고 데이터베이스
쿼리 일부분으로인식하여 데이터베이스의 정보가 노출되거나 인증이 우회되는 
취약점이다. <br>
SQL 인젝션은 사용자가 데이터를 입력할 수 있는 곳 어디에서든 발생할 수 있다.

### GET/Search

* SQL 인젝션이 가능한지 확인
> SELECT * FROM movies WHERE title LIKE ' ' ' <br>
==> ' 를 사용하는 이유 <br> :: 데이터베이스에서 작음따옴표로 문자데이터를
                              구분하기 떄문이다.

![SQL 인젝션 가능여부 확인](https://user-images.githubusercontent.com/76092057/103431891-ce5d1700-4c1a-11eb-9b66-b619954a55a3.PNG){: width:"100%" height:"100%"}

==> 오류 메세지에는 데이터베이스 서버 정보가 포함되는데, 데이터베이스
서버의 종류에 따라 SQL 구문이 다르므로 가장 먼저 서버 정보를 확인<br>
@@ 현재 : MySQL

* 쿼리를 입력하여 어떤 주석 문자를 사용하는지 확인 <br> ==> 쿼리 결과를 항상
참으로 만들고 기존 코드의 뒷부분을 주석 처리한다.

1. ' or 1=1--
2. ' or 1=1#

![SQL 쿼리 성공](https://user-images.githubusercontent.com/76092057/103432134-25182000-4c1e-11eb-8cab-69f34d819943.PNG){: width:"100%" height:"100%"}
@@ 결과 :: 첫번째 쿼리에서는 오류, 두번째 쿼리는 모든 영화 자료가 출력된다.


* 더 자세한 정보를 알아내기 위해 UNION SELECT 구문을 사용<br>
==> UNION :: SELECT 문이 둘 이상일 때 이를 결합하여 두 질의의 결과를
하나로 반환한다. (UNION Based SQL Injection)

> UNION SELECT ALL 1# <br>
==> UNION 구문을 사용하기 위해서는 SELECT 문의 칼럼수가 일치해야함
> ' UNION SELECT ALL 1,2,3,4,5,6,7# <br>
==> 칼럼을 계속 추가하여 확인
![SQL 인젝션 UNION 문](https://user-images.githubusercontent.com/76092057/103432258-b340d600-4c1f-11eb-9645-821ad117feab.PNG){: width:"100%" height:"100%"}
> 0' UNION SELECT ALL 1,@@version,3,4,5,6,7# <br>
==> MySQL 버전을 확인하기 위하여 시스템 변수나 시스템 함수를 활용하여 쿼리 입력




