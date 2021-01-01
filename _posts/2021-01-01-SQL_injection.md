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
==> MySQL 버전을 확인하기 위하여 시스템 변수나 시스템 함수를 활용하여 쿼리 입력,
페이지에 노출되는 칼럼은 2,3,4,5번에 위치함으로 이중 하나에 시스템 변수를 삽입

![SQL 인젝션 MySQL 버전 확인](https://user-images.githubusercontent.com/76092057/103432327-7aedc780-4c20-11eb-921d-2365db1547a9.PNG){: width:"100%" height:"100%"}

@@ 버전 : 5.0.96

* information_schema를 사용하여 테이블 명을 확인
  > 0' UNION SELECT ALL 1,table_name,3,4,5,6,7 from information_schema.tables# 
![SQL 인젝션 모든 테이블명](https://user-images.githubusercontent.com/76092057/103432398-81c90a00-4c21-11eb-842a-f34de5eb7b17.PNG){: width:"100%" height:"100%"}

* 출력한 정보를 토대로 users 테이블에 사용자 계정 정보가 들어있음을 추측, 
  where 절로 users 테이블 정보만 출력하게 조건을 지정한다.
  > 0' UNION SELECT ALL 1,column_name,3,4,5,6,7 from information_schema.columns where table_name='users'#

![SQL 인젝션 WHERE 문](https://user-images.githubusercontent.com/76092057/103432468-a4a7ee00-4c22-11eb-8254-66ca335473f2.PNG){: width:"100%" height:"100%"}

* 페이지에 노출된 칼럼 수보다 확인하려는 칼럼 수가 많을 때는 concat 함수를 사용
  > 0' UNION SELECT ALL 1,concat (id,login), password,email,secret,6,7 from users#

![SQl 인젝션 공격 성공(GET)](https://user-images.githubusercontent.com/76092057/103432520-7840a180-4c23-11eb-8886-8c04c9fc829e.PNG){: width:"100%" height:"100%"}

### 대응방안
![SQL 인젝션 대응방안(GET)](https://user-images.githubusercontent.com/76092057/103432541-c48be180-4c23-11eb-94c6-e6550a3c8d61.PNG){: width:"100%" height:"100%"}

작은따옴표(')를 입력하여도 오류 메세지가 나오지 않으면 SQL Injection 이 불가능하다.
PHP 기본 제공 함수인 mysql_real_escape_strings 함수를 사용하여 입력한 데이터를
우회한다. 이때 이 함수는 사용자 입력 값에 SQL 문법에서 사용하는 특수문자가 있을 경우
백슬래시를 붙여 입력 데이터를 SQl 문법으로 인식하지 않게 방어한다.







