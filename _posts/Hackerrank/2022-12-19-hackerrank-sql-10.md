---
title:  "[해커랭크 SQL] Weather Observation Station 5"
layout: single

categories: "Algorithm_SQL"
tags: ["LENGTH", "UNION"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 EASY 문제 풀이</small>

***

# Weather Observation Station 5
Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

[Weather Observation Station 5 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-5/problem?isFullScreen=true)

## (1) 테이블 정보
The **STATION** table is described as follows:

|Field|Type|
|:----|:---|
|ID| NUMBER|
|CITY| VARCHAR2(21)|
|STATE| VARCHAR2(2)|
|LAT_N |NUMBER|
|LONG_W| NUMBER|

<small>cf. where LAT_N is the northern latitude and LONG_W is the western longitude.</small>

## (2) 문제 이해
가장 짧은 CITY 이름과 가장 긴 CITY 이름과 각각의 길이를 출력하는 쿼리를 작성한다.

## (3) 코드 작성
### UNION 사용O
```sql
(SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY), CITY
LIMIT 1)

UNION

(SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY) DESC, CITY
LIMIT 1)
```

### UNION 사용X
```sql
SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY), CITY
LIMIT 1;

SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY) DESC, CITY
LIMIT 1;
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_10.png" width="85%">
</div>
<center><small>위 두 쿼리의 실행 결과(동일)</small></center>

<br>

## (4) 코드 리뷰
- 문자열의 길이를 불러오기 위해 LENGTH 함수를 사용했다.
- 조건이 다른 두 항목을 출력해야하기 때문에 두개의 쿼리문을 작성하고 UNION으로 연결해 주었다. 하지만 UNION 없이 두 개의 쿼리문을 작성해도 정답 sign을 받을 수 있다.
- ORDER BY, LIMIT를 이용해서 각 경우에 따라 특정 데이터만 가져왔다.
  - 길이가 짧은 경우 : LENGTH(CITY)를 기준으로 오름차순 후 상위 1개
  - 길이가 긴 경우 : LENGTH(CITY)를 기준으로 내림차순 후 상위 1개

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}