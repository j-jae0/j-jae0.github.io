---
title:  "[해커랭크 SQL] Weather Observation Station 12"
layout: single

categories: "Algorithm_SQL"
tags: ["DISTINCT", "NOT LIKE", "REGEXP"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 EASY 문제 풀이</small>

***

# Weather Observation Station 12
Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.

[Weather Observation Station 12 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-12/problem?isFullScreen=true)

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
모음으로 시작되지 않고 모음으로 끝나지 않는 도시명을 중복 제거하여 출력하는 쿼리를 작성한다.

## (3) 코드 작성
### LIKE 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY NOT LIKE 'a%'
  AND CITY NOT LIKE 'e%'
  AND CITY NOT LIKE 'i%'
  AND CITY NOT LIKE 'o%'
  AND CITY NOT LIKE 'u%'
  AND CITY NOT LIKE '%a'
  AND CITY NOT LIKE '%e'
  AND CITY NOT LIKE '%i'
  AND CITY NOT LIKE '%o'
  AND CITY NOT LIKE '%u'
```

### REGEXP 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[^aeiou]' AND CITY REGEXP '[^aeiou]$'
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_17.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (4) 코드 리뷰
모음으로 시작되지 않고 모음으로 끝나지 않는 도시명을 출력하기 위해 두 조건식을 모두 만족하기 위해 OR이 아닌 AND로 연결해 주었다. 

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}