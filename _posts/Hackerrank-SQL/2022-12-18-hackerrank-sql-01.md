---
title:  "[해커랭크 SQL] Basic Select 문제풀이 (1)"
layout: single

categories: "Algorithm_SQL"
tags: ["WHERE"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 EASY 6 문제 풀이</small>

***

# 📄 테이블 정보
The **CITY** table is described as follows:

|Field|Type|
|:----|:---|
|ID| NUMBER|
|NAME| VARCHAR2(17)|
|COUNTRYCODE| VARCHAR2(3)|
|DISTRICT| VARCHAR2(20)|
|POPULATION |NUMBER|

<br>

# 1. Select All
Query all columns (attributes) for every row in the CITY table.<br>
[📍 Select All 문제 보러가기](https://www.hackerrank.com/challenges/select-all-sql/problem?isFullScreen=true)

## (1) 문제 이해
CITY 테이블의 모든 행에 대한 모든 열 출력하는 쿼리를 작성한다.

## (2) 코드 작성
```sql
SELECT *
FROM CITY
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_1.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

## (3) 코드 리뷰
테이블의 전체 요소를 불러오기 위해 *(별표)를 사용했다. *를 SELECT 문에 사용하면 테이블의 모든 필드를 선택하여 불러올 수 있다.

<br>

# 2. Select By ID
Query all columns for a city in CITY with the ID 1661.<br>
[📍 Select By ID 문제 보러가기](https://www.hackerrank.com/challenges/select-by-id/problem?isFullScreen=true)

## (1) 문제 이해
테이블에서 ID가 1661인 모든 데이터 출력하는 쿼리를 작성한다.

## (2) 코드 작성
```sql
SELECT *
FROM CITY
WHERE ID = 1661
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_2.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

## (3) 코드 리뷰
CITY 테이블에서 ID 값이 1661 인 데이터만 불러오기 위해 WHERE 절에서 ID가 1661이다 라는 조건식을 넣었다. 그리고 SELECT 문에 *를 넣어 조건식에 해당하는 행의 모든 열이 출력되도록 쿼리를 작성했다.

<br>

# 3. Japanese Cities' Attributes
Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.<br>
[📍 Japanese Cities' Attributes 문제 보러가기](https://www.hackerrank.com/challenges/japanese-cities-attributes/problem?isFullScreen=true)

## (1) 문제 이해
COUNTRYCODE가 JPN인 데이터의 모든 열 출력하는 쿼리를 작성한다.

## (2) 코드 작성
```sql
SELECT *
FROM CITY
WHERE COUNTRYCODE = 'JPN'
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_3.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

## (3) 코드 리뷰
테이블에서 컨트리코드가 JPN인 데이터의 모든 필드를 출력하는 것이기 때문에 WHERE 절에 COUNTRYCODE가 JPN이라는 조건식을 넣었다. SELECT 문에 *를 넣어 조건식에 맞는 행의 모든 열을 출력할 수 있도록 쿼리를 작성했다.

<br>

# 4. Japanese Cities' Names
Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.<br>
[📍 Japanese Cities' Names 문제 보러가기](https://www.hackerrank.com/challenges/japanese-cities-name/problem?isFullScreen=true)

## (1) 문제 이해
COUNTRYCODE가 JPN인 데이터의 NAME를 출력하는 쿼리를 작성한다.

## (2) 코드 작성
```sql
SELECT NAME
FROM CITY
WHERE COUNTRYCODE = 'JPN'
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_4.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

## (3) 코드 리뷰
WHERE 절에 컨트리코드가 JPN이다 라는 조건식을 넣어 행을 필터링해주었다. 그리고 SELECT 문에 NAME 을 작성하여 모든 컬럼이 출력되지 않고 컬럼이 NAME만 출력될 수 있도록 쿼리를 작성했다.

<br>

# 5. Revising the Select Query I
Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.<br>
[📍 Revising the Select Query I 문제 보러가기](https://www.hackerrank.com/challenges/revising-the-select-query/problem?isFullScreen=true)

## (1) 문제 이해
인구가 100000보다 크고 CONTRYCODE가 USA인 데이터의 모든 열을 출력하는 쿼리를 작성한다.

## (2) 코드 작성
```sql
SELECT *
FROM CITY 
WHERE POPULATION > 100000 AND COUNTRYCODE = 'USA'
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_5.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

## (3) 코드 리뷰
이번 문제는 두 조건을 만족하는 데이터의 모든 열을 불러오는 것이다. 두 조건을 모두 만족하는 행만 불러오기 위해 AND로 두 조건을 연결해주었다. 그리고 모든 컬럼을 불러올 수 있도록 SELECT 문에 *를 입력했다.

<br>

# 6. Revising the Select Query II
Query the NAME field for all American cities in the CITY table with populations larger than 120000. The CountryCode for America is USA.<br>
[📍 Revising the Select Query II 문제 보러가기](https://www.hackerrank.com/challenges/revising-the-select-query-2/problem?isFullScreen=true)

## (1) 문제 이해
인구가 120000보다 크고 CONTRYCODE가 USA인 데이터의 NAME을 출력하는 쿼리를 작성한다.

## (2) 코드 작성
```sql
SELECT NAME
FROM CITY 
WHERE POPULATION > 120000 AND COUNTRYCODE = 'USA'
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_6.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

## (3) 코드 리뷰
문제는 두 조건을 만족하는 데이터의 NAME을 불러오는 것이다. 두 조건을 모두 만족하는 행만 불러오기 위해 AND로 두 조건을 연결해주었다. 조건식에 의해 필터링된 행의 NAME(이름)만 불러오기 위해 SELECT 문에 NAME을 작성했다.

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}