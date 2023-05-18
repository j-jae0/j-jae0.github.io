---
title:  "[해커랭크 SQL] Advanced Join 문제풀이 (3)"
layout: single

categories: "Algorithm_SQL"
tags: [""]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 MEDIUM 1 문제 풀이</small>

***

# 1. SQL Project Planning
If the End_Date of the tasks are consecutive, then they are part of the same project. Samantha is interested in finding the total number of different projects completed.

Write a query to output the start and end dates of projects listed by the number of days it took to complete the project in ascending order. If there is more than one project that have the same number of completion days, then order by the start date of the project.

[📍 SQL Project Planning 문제 보러가기](https://www.hackerrank.com/challenges/sql-projects/problem?isFullScreen=true)

## (1) 테이블 정보
You are given a table, Projects, containing three columns: Task_ID, Start_Date and End_Date. It is guaranteed that the difference between the End_Date and the Start_Date is equal to 1 day for each row in the table.

| Column | Type |
|:-------|:-----|
| Task_ID | Integer |
| Start_Date | Date |
| End_Date | Date |

## (2) 문제 이해
테이블엔 작업의 아이디, 작업의 시작일과 종료일이 담겨있다. 프로젝트의 완료일이 연속적이면 동일한 프로젝트의 일부이다. (예: 2023-01-01 ~ 2023-01-02와 2023-01-02 ~ 2023-01-03 은 동일한 프로젝트) 프로젝트별로 시작일과 종료일을 출력한다.(동일한 프로젝트라면 하나로 합쳐야 함) 결과는 프로젝트를 완료하는데 걸린 일수를 기준으로 오름차순 정렬하고 만약 소요된 일수가 같다면 시작일을 기준으로 오름차순 정렬한다.

## (3) 코드 작성
```sql
SELECT start_date, MIN(end_date)
FROM (SELECT start_date
      FROM Projects 
      WHERE start_date NOT IN (SELECT end_date FROM Projects)) AS T1,
      (SELECT end_date
      FROM Projects
      WHERE end_date NOT IN (SELECT start_date FROM Projects)) AS T2
WHERE start_date < end_date
GROUP BY start_date
ORDER BY DATEDIFF(MIN(end_date), start_date), start_date
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_22_1.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (4) 코드 리뷰
문제를 풀기 위해 테이블을 먼저 출력해서 어떻게 접근하면 좋을지 고민해 보았다.

```sql
SELECT start_date, end_date
FROM Projects
ORDER BY start_date
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_22_2.png" width="65%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

위 이미지와 같이 만약 End_date와 Start_date가 같을 경우 동일한 프로젝트로 묶어서 시작일과 프로젝트 최종! 종료일로 출력해야 한다. JOIN을 하는 것은 적절하지 않다고 판단되었다. 불러와야하는 Start_Date는 End_Date에 같은 일자가 기록되어있다면 생략하고 End_Date와 Start_Date가 같지 않는 경우를 불러와야한다. End_Date 역시 Start_Date와 같은 일자가 기록되어있다면 생략하고 Start_Date와 같지 않는 경우를 불러와야한다. 그래서 FROM 문에 테이블을 두개 불러오기로 결정했다.(start_date, end_date)

- T1: 종료일과 같지 않은 시작일을 불러온다.
- T2: 시작일과 같지 않은 종료일을 불러온다.

```sql
-- 종료일에 포함되지 않는 시작일만 불러옴
SELECT start_date
FROM (SELECT start_date
      FROM Projects 
      WHERE start_date NOT IN (SELECT end_date FROM Projects)) AS T1
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_22_3.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

```sql
-- 시작일에 포함되지 않는 종료일 불러옴
SELECT end_date
FROM (SELECT end_date
      FROM Projects
      WHERE end_date NOT IN (SELECT start_date FROM Projects)) AS T2
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_22_4.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

```sql
SELECT start_date, end_date
FROM (SELECT start_date
      FROM Projects 
      WHERE start_date NOT IN (SELECT end_date FROM Projects)) AS T1,
      (SELECT end_date
      FROM Projects
      WHERE end_date NOT IN (SELECT start_date FROM Projects)) AS T2
ORDER BY start_date, end_date
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_22_5.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

서브쿼리로 두 테이블을 불러왔을 때, 위 이미지를 보면 한 start_date에 대해 모든 end_date의 조합이 생성된 것을 볼 수 있다. JOIN 없이 ,로 테이블을 가져오면 모든 조합의 데이터가 생성된다.<br>

이러한 이유로 WHERE 절에 시작일이 종료일보다 작아야한다는 조건문을 작성하였고 시작일을 기준으로 그룹화, 종료일은 최솟값으로 불러왔다. 마지막으로 정렬은 시작일과 종료일의 차이를 기준으로 오름차순, 시작일을 기준으로 오름차순 정렬하였다.<br>

<u>시작일을 기준으로 그룹화 후, 종료일을 불러오려면 그룹 함수를 사용해야한다. 그래서 MIN 함수를 사용했다.</u>


👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}