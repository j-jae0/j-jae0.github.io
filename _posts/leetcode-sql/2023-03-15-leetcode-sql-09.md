---
title:  "[리트코드 SQL] Day 8. Function"
layout: single

categories: "Algorithm_SQL"
tags: [""]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"

published: false
---

<small>SQL I : Day 8 Function 4문제 풀이</small>

***

# <span class="half_HL">586. Customer Placing the Largest Number of Orders</span>

## (1) 코드 작성
```sql
SELECT IF(customer_number is not null, MAX(customer_number)) as customer_number
FROM Orders
```

## (2) 코드 리뷰 및 회고
- 
- [👉 문제 보러가기](https://leetcode.com/problems/customer-placing-the-largest-number-of-orders/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">511. Game Play Analysis I</span>

## (1) 코드 작성
```sql
SELECT player_id
     , MIN(event_date) AS first_login
FROM Activity
GROUP BY player_id
```

## (2) 코드 리뷰 및 회고
- 
- [👉 문제 보러가기](https://leetcode.com/problems/game-play-analysis-i/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1890. The Latest Login in 2020</span>

## (1) 코드 작성
```sql
SELECT user_id
     , MAX(time_stamp) AS last_stamp
FROM Logins
WHERE YEAR(time_stamp) = '2020'
GROUP BY user_id
```

## (2) 코드 리뷰 및 회고
- 
- [👉 문제 보러가기](https://leetcode.com/problems/the-latest-login-in-2020/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1741. Find Total Time Spent by Each Employee</span>

## (1) 코드 작성
```sql
SELECT event_day AS day
     , emp_id
     , SUM(out_time - in_time) AS total_time
FROM Employees
GROUP BY event_day, emp_id
```

## (2) 코드 리뷰 및 회고
- 
- [👉 문제 보러가기](https://leetcode.com/problems/find-total-time-spent-by-each-employee/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}