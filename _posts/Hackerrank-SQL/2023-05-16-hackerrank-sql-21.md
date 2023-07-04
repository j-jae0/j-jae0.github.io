---
title:  "[해커랭크 SQL] Advanced Join 문제풀이 (2)"
layout: single

categories: "Algorithm_SQL"
tags: ["JOIN"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 MEDIUM 1 문제 풀이</small>

***

# 1. Placements
Write a query to output the names of those students whose best friends got offered a higher salary than them. Names must be ordered by the salary amount offered to the best friends. It is guaranteed that no two students got same salary offer.

[📍 Placements 문제 보러가기](https://www.hackerrank.com/challenges/placements/problem?isFullScreen=true)

## (1) 테이블 정보
**Students** contains two columns: ID and Name. 

| Column | Type |
|:-------|:-----|
| ID | Integer |
| Name | String |

**Friends** contains two columns: ID and Friend_ID (ID of the ONLY best friend). 

| Column | Type |
|:-------|:-----|
| ID | Integer |
| Friend_ID | Integer |

**Packages** contains two columns: ID and Salary (offered salary in $ thousands per month).

| Column | Type |
|:-------|:-----|
| ID | Integer |
| Salary | Float |

## (2) 문제 이해
문제는 가장 친한 친구보다 낮은 급여를 받은 학생의 이름을 출력하는 것이다. Friends 테이블을 보면 절친의 아이디 값이 나온다. 친구보다 더 낮은 급여를 받은 학생의 이름을 출력한다. 이때 결과는 친구의 급여를 기준으로 오름차순 정렬한다.

## (3) 코드 작성
```sql
SELECT Name
FROM Students AS S
JOIN Friends AS F ON S.ID = F.ID
JOIN Packages AS P1 ON S.ID = P1.ID
JOIN Packages AS P2 ON F.Friend_ID = P2.ID
WHERE P1.Salary < P2.Salary
ORDER BY P2.Salary
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_21_1.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (4) 코드 리뷰
- 내 급여와 친구의 급여 정보를 불러오기 위해 급여 정보가 담긴 Packages 테이블을 P1, P2로 각각 내 급여, 친구 급여로 붙여주었다.
- 테이블을 결합하고 친구가 더 높은 급여를 받았다는 조건을 WHERE 절에 추가했다.
  - 친구보다 낮은 급여를 받은 데이터만 남게 됨
- 결과는 친구의 급여를 기준으로 오름차순 정렬하였고 학생의 이름만 출력할 수 있도록 SELECT 문에 Name만 넣어주었다.
- EASY 😎

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}