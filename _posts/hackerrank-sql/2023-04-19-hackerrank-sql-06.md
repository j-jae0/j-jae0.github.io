---
title:  "[해커랭크 SQL] Basic Select 문제풀이 (3)"
layout: single

categories: "Algorithm_SQL"
tags: ["RIGHT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, EASY 3 문제 풀이</small>

***

# <span class="half_HL">✔️ 테이블 정보</span>

The ```EMPLOYEE``` table containing employee data for a company is described as follows:

| Column | Type |
|:-----|:-----|
| employee_id | Integer |
| name | String |
| months | Integer |
| salary | Integer |

where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company, and salary is the their monthly salary.

The ```STUDENTS``` table is described as follows:

| Column | Type |
|:-----|:-----|
| ID | Integer |
| Name | String |
| Marks | Integer |

<br>

# 1. Employee Names
Write a query that prints a list of employee names (i.e.: the name attribute) from the ```Employee``` table in alphabetical order.

**문제 요약** : ```Employee``` 테이블에서 알파벳순으로 직원 이름 목록(예: name 특성)을 불러오는 쿼리를 작성하세요.

## (1) 코드 작성
```sql
SELECT name
FROM Employee
ORDER BY name
```

[👉 Employee Names 문제 보러가기](https://www.hackerrank.com/challenges/name-of-employees/problem?isFullScreen=true)

<br>

# 2. Employee Salaries
Write a query that prints a list of employee names (i.e.: the name attribute) for employees in ```Employee``` having a salary greater than $2000 per month who have been employees for less than 10 months. Sort your result by ascending employee_id.

**문제 요약** : 월급이 $2000 이상이고 근무 기간이 10개월 미만인 Employee의 직원에 대한 직원 이름(즉, 이름 속성) 목록을 인쇄하는 쿼리를 작성하고 employee_id를 오름차순으로 결과를 정렬하세요.

## (1) 코드 작성
```sql
SELECT name
FROM Employee
WHERE salary > 2000 AND months < 10
ORDER BY employee_id
```

[👉 Employee Salaries 문제 보러가기](https://www.hackerrank.com/challenges/salary-of-employees/problem?isFullScreen=true)

<br>

# 3. Higher Than 75 Marks
Query the Name of any student in ```STUDENTS``` who scored higher than 75 Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

**문제 요약** : ```STUDENTS```에서 75점보다 높은 점수를 받은 학생의 이름을 불러오는데, 이름의 마지막 세 문자를 기준으로 정렬하세요. 이때 두 명 이상의 학생 모두 이름이 마지막 세 글자로 끝나는 경우(예: Bobby, Robby 등) ID를 오름차순으로 2차 정렬하세요.

## (1) 코드 작성
```sql
SELECT Name
FROM STUDENTS
WHERE Marks > 75
ORDER BY RIGHT(Name, 3), ID
```

[👉 Higher Than 75 Marks 문제 보러가기](https://www.hackerrank.com/challenges/more-than-75-marks/problem?isFullScreen=true)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}