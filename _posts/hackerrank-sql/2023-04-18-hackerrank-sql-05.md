---
title:  "[해커랭크 SQL] AGGREGATION 문제풀이 (3)"
layout: single

categories: "Algorithm_SQL"
tags: ["FLOOR", "CEIL", "AVG", "SUM", "MAX", "MIN", "REPLACE", "COUNT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, EASY 5 문제 풀이</small>

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

The ```EMPLOYEES``` table is described as follows:

|Column|Type|
|:-----|:---|
|ID|Integer|
|Name|String|
|Salary|Integer|

**Note**: Salary is per month. <br>
**Constraints**: 1000 < Salary < 10^5

The ```EMPLOYEE``` table is described as follows:

|Column|Type|
|:-----|:---|
| employee_id | Integer |
| name | String |
| months | Integer |
| salary | Integer |

where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company, and salary is the their monthly salary.

<br>

# 1. Average Population
Query the average population for all cities in ```CITY```, rounded down to the nearest integer.

**문제 요약** : ```CITY```에 있는 모든 도시의 평균 인구를 가장 가까운 정수로 내림하세요.

## (1) 코드 작성
```sql
SELECT FLOOR(AVG(POPULATION))
FROM CITY
```

[👉 Average Population 문제 보러가기](https://www.hackerrank.com/challenges/average-population/problem?isFullScreen=true)

<br>

# 2. Japan Population
Query the sum of the populations for all Japanese cities in ```CITY```. The COUNTRYCODE for Japan is ```JPN```.

**문제 요약** : ```CITY```에 있는 모든 일본 도시의 인구 합계를 구하세요.

## (1) 코드 작성
```sql
SELECT SUM(POPULATION)
FROM CITY
WHERE COUNTRYCODE = 'JPN'
```

[👉 Japan Population 문제 보러가기](https://www.hackerrank.com/challenges/japan-population/problem?isFullScreen=true)

<br>

# 3. Population Density Difference
Query the difference between the maximum and minimum populations in ```CITY```.

**문제 요약** : ```CITY```의 최대 인구와 최소 인구 간의 차이를 구하세요.

## (1) 코드 작성
```sql
SELECT MAX(POPULATION) - MIN(POPULATION)
FROM CITY
```

[👉 Population Density Difference 문제 보러가기](https://www.hackerrank.com/challenges/population-density-difference/problem?isFullScreen=true)

<br>

# 4. The Blunder
Samantha was tasked with calculating the average monthly salaries for all employees in the ```EMPLOYEES``` table, but did not realize her keyboard's 0 key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with any zeros removed), and the actual average salary.

Write a query calculating the amount of error (i.e.: **actual** - **miscalculated** average monthly salaries), and round it up to the next integer.

**문제 요약** : 직원의 평균 월급을 계산하는 Samantha는 키보드의 0키가 고장나서 0이 제거된 급여로 평균을 구했다. 구하고자 하는 것은 0이 제거되지 않은 원래 구해야되는 평균 월급과 0이 제거된(잘못 계산된) 급여의 평균값의 차를 구하고 이를 올림하여 정수로 구하는 것이다.

## (1) 코드 작성
```sql
SELECT CEIL(AVG(SALARY)-AVG(REPLACE(SALARY, 0, '')))
FROM EMPLOYEES
```

[👉 The Blunder 문제 보러가기](https://www.hackerrank.com/challenges/the-blunder/problem?isFullScreen=true)

<br>

# 5. Top Earners
We define an employee's total earnings to be their monthly **salary** * **months** worked, and the maximum total earnings to be the maximum total earnings for any employee in the ```Employee``` table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as 2 space-separated integers.

**문제 요약** : 직원의 총 소득을 구하고 직원들 중 최대 총 소득과 그 소득을 보유한 사람의 수를 구하는 것이다.

## (1) 코드 작성
```sql
SELECT SALARY*MONTHS, COUNT(*)
FROM EMPLOYEE
GROUP BY SALARY*MONTHS
ORDER BY SALARY*MONTHS DESC
LIMIT 1
```

[👉 Top Earners 문제 보러가기](https://www.hackerrank.com/challenges/earnings-of-employees/problem?isFullScreen=true)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}