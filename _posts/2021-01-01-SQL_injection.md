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
> SELECT * FROM movies WHERE title LIKE ' ' '
==> ' 를 사용하는 이유 <br> :: 데이터베이스에서 작음따옴표로 문자데이터를
                              구분하기 떄문이다.

![SQL 인젝션 가능여부 확인](https://user-images.githubusercontent.com/76092057/103431891-ce5d1700-4c1a-11eb-9b66-b619954a55a3.PNG){: width:"100%" height:"100%"}

==> 오류 메세지에는 데이터베이스 서버 정보가 포함되는데, 데이터베이스
서버의 종류에 따라 SQL 구문이 다르므로 가장 먼저 서버 정보를 확인<br>
* 현재 : MySQL

* 쿼리를 입력하여 어떤 주석 문자를 사용하는지 확인

<table>
  <tr>
    <td>쿼리</td>
    <td>뜻</td>
  </tr>
  <tr>
    <td colspan="2">내용</td>
  </tr>
</table>


