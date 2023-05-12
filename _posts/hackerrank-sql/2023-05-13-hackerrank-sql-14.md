---
title:  "[해커랭크 SQL] Advanced Select 문제풀이 (5)"
layout: single

categories: "Algorithm_SQL"
tags: ["JOIN", "COUNT", "DISTINCT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, MEDIUM 1 문제 풀이</small>

***

# 1. New Companies

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_14_1.png" width="90%">
</div>

[👉 New Companies 문제 보러가기](https://www.hackerrank.com/challenges/the-company/problem?isFullScreen=true)

## (1) 테이블
The following tables contain company data:

**Company**: The company_code is the code of the company and founder is the founder of the company. 

| Column | Type |
|:-------|:-----|
| company_code | string |
| founder | String |

**Lead_Manager**: The lead_manager_code is the code of the lead manager, and the company_code is the code of the working company.

| Column | Type |
|:-------|:-----|
| lead_manager_code | String |
| company_code | string |

**Senior_Manager**: The senior_manager_code is the code of the senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company. 

| Column | Type |
|:-------|:-----|
| senior_manager_code | String |
| lead_manager_code | String |
| company_code | string |

**Manager**: The manager_code is the code of the manager, the senior_manager_code is the code of its senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company. 

| Column | Type |
|:-------|:-----|
| manager_code | String |
| senior_manager_code | String |
| lead_manager_code | String |
| company_code | string |

**Employee**: The employee_code is the code of the employee, the manager_code is the code of its manager, the senior_manager_code is the code of its senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.

| Column | Type |
|:-------|:-----|
| employee_code | String|
| manager_code | String |
| senior_manager_code | String |
| lead_manager_code | String |
| company_code | string |

## (2) 문제 이해
- 각 회사에 대해 직급별로 몇명이 존하는지를 출력해야 한다.
- Employee 테이블을 보면 전체 직급에 대한 컬럼이 존재하지만 단독으로 사용하면 정답을 구할 수 없다.
  - 존재하는 직원의 데이터만 존재
  - A, B라는 직원이 특정 매니저에 소속된 구조
  - 직원이 연결되어있지 않은 관리자가 존재할 수 있음(각 직급별 전체 관리자의 수를 구할 수 없음)
- 위와같은 이유로 전체 테이블을 회사코드를 기준으로 JOIN하여 유니크한 직급코드의 개수를 불러온다.(중복된 경우가 있음)

## (3) 코드 작성
```sql
SELECT c.company_code, 
       c.founder,
       COUNT(DISTINCT l.lead_manager_code) AS num_lm,
       COUNT(DISTINCT s.senior_manager_code) AS num_sm,
       COUNT(DISTINCT m.manager_code) AS num_m,
       COUNT(DISTINCT e.employee_code) AS num_e
FROM Company AS c
INNER JOIN Lead_Manager AS l ON c.company_code = l.company_code
INNER JOIN Senior_Manager AS s ON c.company_code = s.company_code
INNER JOIN Manager AS m ON c.company_code = m.company_code
INNER JOIN Employee AS e ON c.company_code = e.company_code
GROUP BY c.company_code, c.founder
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_14_2.png" width="75%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (4) 코드 리뷰
- 각 회사 정보(회사 코드, 설립명)가 담긴 Company 테이블에 각 관리자, 직원의 코드가 담긴 테이블을 JOIN하여 연결해 주었다.
  - 회사별로 관리자, 직원의 코드를 연결하는 개념
- 회사별 관리자, 직원의 수를 불러와야하기 때문에 코드, 설립명을 기준으로 그룹화하였다.(이때 컬럼에 설립명을 쓰려면 그룹화 필요)
- 수를 구할 땐 중복되는 레코드가 존재할 수 있다는 점에서 COUNT로 직원 및 관리자 수를 구할 때 DISTINCT 로 중복을 제외하고 카운팅 하였다.
- EASY 😎

## (5) 회고
다만 아쉬운 점은 이전 문제들 대비 실행속도가 느렸다. 아무래도 JOIN을 여러번 사용해서 그런 것같다. 실제로 회사에서 이런식으로 데이터를 나누어서 저장을 하고있다면 데이터를 불러오는데 더 많은 시간이 소요될 것같다. 조금 더 시간을 단축시킬 수 있는 방법이 없을까? 다른 쿼리 작성법도 알아봐야겠고 만약 내가 데이터 시스템을 구축한다면 어떻게 구축해야 불러올 때 가볍게 효율적으로 불러올 수 있는지를 공부해 봐야겠다!

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}