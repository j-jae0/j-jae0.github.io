---
title:  "[해커랭크 SQL] Basic Join 문제풀이 (1)"
layout: single

categories: "Algorithm_SQL"
tags: ["JOIN", "SUM", "FLOOR", "AVG"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, EASY 3 문제 풀이</small>

***

# ✔️ 테이블 정보
The ```CITY``` table are described as follows:

| Field | Type |
|:------|:-----|
| ID | NUMBER |
| NAME | VARCHAR2 (17) |
| COUNTRYCODE | VARCHAR2 (3) |
| DISTRICT | VARCHAR2 (20) |
| POPULATION | NUMBER |

The ```COUNTRY``` table are described as follows:

| Field | Type |
|:------|:-----|
| CODE | VARCHAR2 (3) |
| NAME | VARCHAR2 (44) |
| CONTINENT | VARCHAR2 (13) |
| REGION | VARCHAR2 (25) |
| SURFACEAREA | NUMBER |
| INDEPYEAR | VARCHAR2 (5) |
| POPULATION | NUMBER |
| LIFEEXPECTANCY | VARCHAR2 (4) |
| GNP | NUMBER |
| GNPOLD | VARCHAR2 (9) |
| LOCALNAME | VARCHAR2 (44) |
| GOVERNMENTFORM | VARCHAR2 (44) |
| HEADOFSTATE | VARCHAR2 (32) |
| CAPITAL | VARCHAR2 (4) |
| CODE2 | VARCHAR2 (2) |

**참고**: ```CITY.CountryCode``` 와 ```COUNTRY.Code``` 는 동일한 컬럼이다.

<br>

# 1. Population Census
Given the ```CITY``` and ```COUNTRY``` tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.

**문제 요약** : CONTINENT가 'Asia'인 모든 도시의 인구 합계를 불러온다.

## (1) 코드 작성
```sql
SELECT SUM(T2.population)
FROM COUNTRY AS T1
INNER JOIN CITY AS T2 ON T1.code = T2.countrycode
WHERE T1.continent = 'Asia'
```

[👉 Population Census 문제 보러가기](https://www.hackerrank.com/challenges/asian-population/problem?isFullScreen=true)

<br>

# 2. African Cities
Given the ```CITY``` and ```COUNTRY``` tables, query the names of all cities where the CONTINENT is 'Africa'.

**문제 요약** : CONTINENT가 'Africa'인 모든 도시의 이름을 불러온다.

## (1) 코드 작성
```sql
SELECT T2.name
FROM COUNTRY AS T1
INNER JOIN CITY AS T2 ON T1.code = T2.countrycode
WHERE T1.continent = 'Africa'
```

[👉 African Cities 문제 보러가기](https://www.hackerrank.com/challenges/african-cities/problem?isFullScreen=true)

<br>

# 3. Average Population of Each Continent
Given the ```CITY``` and ```COUNTRY``` tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.

**문제 요약** : 모든 대륙의 이름(```COUNTRY.Continent```)과 각 대륙의 평균 도시 인구(```CITY.Population```)를 가장 가까운 정수로 내림하여 불러온다.

## (1) 코드 작성
```sql
SELECT T2.Continent, FLOOR(AVG(T1.Population))
FROM CITY AS T1
INNER JOIN COUNTRY AS T2 ON T1.CountryCode = T2.Code
GROUP BY T2.Continent
```

[👉 Average Population of Each Continent 문제 보러가기](https://www.hackerrank.com/challenges/average-population-of-each-continent/problem?isFullScreen=true)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}