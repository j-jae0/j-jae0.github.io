---
title:  "[해커랭크 SQL] Revising the Select Query II"
layout: single

categories: "Algorithm_SQL"

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 EASY 문제 풀이</small>

***

# Revising the Select Query II
Query the NAME field for all American cities in the CITY table with populations larger than 120000. The CountryCode for America is USA.

[Revising the Select Query II 문제 보러가기](https://www.hackerrank.com/challenges/revising-the-select-query-2/problem?isFullScreen=true)

## (1) 테이블 정보
The **CITY** table is described as follows:

|Field|Type|
|:----|:---|
|ID| NUMBER|
|NAME| VARCHAR2(17)|
|COUNTRYCODE| VARCHAR2(3)|
|DISTRICT| VARCHAR2(20)|
|POPULATION |NUMBER|

## (2) 문제 이해
인구가 120000보다 크고 CONTRYCODE가 USA인 데이터의 NAME을 출력하는 쿼리를 작성한다.

## (3) 코드 작성
```sql
SELECT NAME
FROM CITY 
WHERE POPULATION > 120000 AND COUNTRYCODE = 'USA'
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_6.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (4) 코드 리뷰
문제는 두 조건을 만족하는 데이터의 NAME을 불러오는 것이다. 두 조건을 모두 만족하는 행만 불러오기 위해 AND로 두 조건을 연결해주었다. 조건식에 의해 필터링된 행의 NAME(이름)만 불러오기 위해 SELECT 문에 NAME을 작성했다.

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}