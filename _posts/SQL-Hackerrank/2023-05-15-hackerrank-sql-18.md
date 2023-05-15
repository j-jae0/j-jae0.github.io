---
title:  "[해커랭크 SQL] Basic Join 문제풀이 (3)"
layout: single

categories: "Algorithm_SQL"
tags: ["JOIN", "NULL"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 MEDIUM 1 문제 풀이</small>

***

# 1. The Report
Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.

Write a query to help Eve.

[📍 The Report 문제 보러가기](https://www.hackerrank.com/challenges/the-report/problem?isFullScreen=true)

## (1) 테이블 정보
You are given two tables: Students and Grades. <br>
**Students** contains three columns ID, Name and Marks.

| Column | Type |
|:-------|:-----|
| ID | Integer |
| Name | String |
| Marks | Integer |

**Grades** contains the following data:

| Grade | Min_Mark | Max_Mark |
|:------|:---------|:---------|
| 1 | 0 | 9 |
| 2 | 10 | 19 |
| 3 | 20 | 29 |
| 4 | 30 | 39 |
| 5 | 40 | 49 |
| 6 | 50 | 59 |
| 7 | 60 | 69 |
| 8 | 70 | 79 |
| 9 | 80 | 89 |
| 10 | 90 | 100 |

## (2) 문제 이해
Students 테이블엔 학생의 아이디, 이름, 점수가 포함되어있고 Grades 테이블엔 등급별 점수대가 포함되어있다. 학생의 점수를 기준으로 등급을 매기고 등급별로 내림차순한다. 이때 등급이 8보다 작은 경우는 이름을 NULL로 표기한다. 정렬방법은 다음과 같다.

- 등급이 8이상일 때: 등급을 기준으로 내림차순, 이름을 기준으로 오름차순
- 등급이 8미만일 때: 등급을 기준으로 내림차순, 점수를 기준으로 오름차순

## (3) 코드 작성
```sql
SELECT T1.name AS name,
       T2.grade AS grade,
       T1.marks AS marks
FROM Students AS T1
INNER JOIN Grades AS T2 ON T1.marks >= T2.min_mark AND T1.marks <= T2.max_mark
WHERE T2.grade >= 8
ORDER BY grade DESC, name;

SELECT NULL AS name,
       T2.grade AS grade,
       T1.marks AS marks
FROM Students AS T1
INNER JOIN Grades AS T2 ON T1.marks >= T2.min_mark AND T1.marks <= T2.max_mark
WHERE T2.grade < 8
ORDER BY grade DESC, marks;
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_18_1.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (4) 코드 리뷰
- 두 개의 쿼리를 작성한 이유는 케이스별로 정렬방법이 다르기 때문이다. 처음엔 UNION으로 두 경우를 붙이려고 했으나 UNION 사용 시, 서브 쿼리의 정렬이 무너지기 때문에 이와같이 쿼리를 작성했다.
  - 참고: [UNION 사용시, 서브쿼리 정렬 무너지는 현상이 담긴 게시물 보기](https://j-jae0.github.io/algorithm_sql/hackerrank-sql-11/#-%EC%8B%A4%ED%8C%A8-%EC%BD%94%EB%93%9C-%EA%B3%B5%EC%9C%A0)
- 등급을 매길 땐, JOIN에서 결합할 기준(ON)에 해당 학생의 점수가 특정 등급의 최저점수 이상, 최대점수 이하 라는 기준을 넣었다.
- 등급이 8미만일 땐, 이름을 NULL로 처리해야해서 name 컬럼에 NULL값이 들어갈 수 있게 작성했다.
- 등급이 8 이상일때와 8 미만일때는 WHERE 문에서 나누어주었다.
- EASY 😎

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}