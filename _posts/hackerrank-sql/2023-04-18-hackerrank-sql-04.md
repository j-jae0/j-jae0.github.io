---
title:  "[해커랭크 SQL] AGGREGATION 문제풀이 (2)"
layout: single

categories: "Algorithm_SQL"
tags: ["COUNT", "SUM", "AVG"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, EASY 3 문제 풀이</small>

***

# <span class="half_HL">✔️ 테이블 정보</span>

The ```CITY``` table is described as follows:

|Field|Type|
|:----|:---|
|ID| NUMBER|
|NAME| VARCHAR2 (17)|
|COUNTRYCODE| VARCHAR2 (3)|
|DISTRICT |VARCHAR2 (20)|
|POPULATION| NUMBER|

<br>

# <span class="half_HL">1. Revising Aggregations - The Count Function</span>
Query a count of the number of cities in ```CITY``` having a Population larger than 100,000.

**문제 요약** : 인구가 100,000보다 큰 ```CITY```의 도시 수를 쿼리

## (1) 코드 작성
```sql
SELECT COUNT(*) AS 'a count of the number of cities'
FROM CITY
WHERE Population > 100000
```

[👉 Revising Aggregations - The Count Function 문제 보러가기](https://www.hackerrank.com/challenges/revising-aggregations-the-count-function/problem?isFullScreen=true)

<br>

# <span class="half_HL">2. Revising Aggregations - The Sum Function</span>
Query the total population of all cities in ```CITY``` where District is California.

**문제 요약** : District가 California인 ```CITY```에 있는 모든 도시의 총 인구를 쿼리

## (1) 코드 작성
```sql
SELECT SUM(POPULATION)
FROM CITY
WHERE DISTRICT = 'California'
```

[👉 Revising Aggregations - The Sum Function 문제 보러가기](https://www.hackerrank.com/challenges/revising-aggregations-sum/problem?isFullScreen=true)

<br>

# <span class="half_HL">3. Revising Aggregations - Averages</span>
Query the average population of all cities in ```CITY``` where District is California.

**문제 요약** : District가 California인 ```CITY```에 있는 모든 도시의 평균 인구를 쿼리

## (1) 코드 작성
```sql
SELECT AVG(POPULATION)
FROM CITY
WHERE DISTRICT = 'California'
```

[👉 Revising Aggregations - Averages 문제 보러가기](https://www.hackerrank.com/challenges/revising-aggregations-the-average-function/problem?isFullScreen=true)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}