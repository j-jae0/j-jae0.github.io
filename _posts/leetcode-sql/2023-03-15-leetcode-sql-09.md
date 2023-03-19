---
title:  "[리트코드 SQL] Day 8. Function"
layout: single

categories: "Algorithm_SQL"
tags: ["COUNT", "MIN", "MAX", "SUM"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL I : Day 8 Function 4문제 풀이</small>

***

# <span class="half_HL">586. Customer Placing the Largest Number of Orders</span>
가장 많은 주문을 한 고객의 ```customer_number```를 찾는 SQL 쿼리를 작성하십시오.<br>
테이블: ```Orders```

| Column Name     | Type     |
|:----------------|:---------|
| order_number    | int      |
| customer_number | int      |

## (1) 코드 작성
```sql
SELECT customer_number
FROM Orders
GROUP BY customer_number
ORDER BY COUNT(*) DESC 
LIMIT 1
```

## (2) 코드 리뷰 및 회고
- 문제는 주문을 가장 많이 한 고객의 정보를 불러오는 것이다. 
- 고객별 주문 횟수를 구하기 위해 ```customer_number```로 그룹화하고 주문횟수를 구하기 위해 집계함수 ```COUNT```를 사용하여 내림차순 정렬한 후 최다 주문자를 불러오기 위해 ```LIMIT```를 사용했다.
- [👉 문제 보러가기](https://leetcode.com/problems/customer-placing-the-largest-number-of-orders/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">511. Game Play Analysis I</span>
각 플레이어의 첫 로그인 날짜를 보고하는 SQL 쿼리를 작성하시오.<br>
테이블: ```Activity```

| Column Name  | Type    |
|:-------------|:--------|
| player_id    | int     |
| device_id    | int     |
| event_date   | date    |
| games_played | int     |

## (1) 코드 작성
```sql
SELECT player_id
     , MIN(event_date) AS first_login
FROM Activity
GROUP BY player_id
```

## (2) 코드 리뷰 및 회고
- 문제를 만족하기 위해 플레이어를 기준으로 그룹화하고 첫 로그인 날짜를 불러오기 위해 집계함수 ```MIN```을 사용했다.
- [👉 문제 보러가기](https://leetcode.com/problems/game-play-analysis-i/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1890. The Latest Login in 2020</span>
2020년 모든 사용자의 최신 로그인을 보고하는 SQL 쿼리를 작성하십시오. 2020년에 로그인하지 않은 사용자는 포함하지 마십시오.<br>
테이블: ```Logins```

| Column Name    | Type     |
|:---------------|:---------|
| user_id        | int      |
| time_stamp     | datetime |

## (1) 코드 작성
```sql
SELECT user_id
     , MAX(time_stamp) AS last_stamp
FROM Logins
WHERE YEAR(time_stamp) = '2020'
GROUP BY user_id
```

## (2) 코드 리뷰 및 회고
- 문제를 만족하기 위해 우선 2020년에 로그인 한 데이터만 불러오기 위해 ```WHERE```에 조건식을 추가했다.
- 유저별로 최신 로그인 정보를 불러오기 위해 유저를 기준으로 그룹화하고 최신 로그인 날짜를 불러오기 위해 ```MAX``` 함수를 사용했다.
- ```MAX``` 함수를 사용하면 해당 날짜 범위(2020년)에서 유저별로 가장 큰 날짜(최신)를 불러 올 수 있다.
- [👉 문제 보러가기](https://leetcode.com/problems/the-latest-login-in-2020/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1741. Find Total Time Spent by Each Employee</span>
각 직원이 매일 사무실에서 보낸 총 시간(분)을 계산하는 SQL 쿼리를 작성하시요. 하루 동안 직원은 두 번 이상 출입할 수 있습니다. 단일 항목에 대해 사무실에서 보낸 시간은 ```out_time - in_time```입니다.<br>
테이블: ```Employees```

| Column Name | Type |
+-------------+------+
| emp_id      | int  |
| event_day   | date |
| in_time     | int  |
| out_time    | int  |

## (1) 코드 작성
```sql
SELECT event_day AS day
     , emp_id
     , SUM(out_time - in_time) AS total_time
FROM Employees
GROUP BY event_day, emp_id
```

## (2) 코드 리뷰 및 회고
- 문제는 날짜별로 직원이 사무실에 보낸 시간을 불러오는 것이다.
- 우선 날짜와 직원을 기준으로 그룹화하고 사무실에서 보낸 시간을 출력하기 위해 ```out_time - in_time```를 ```total_time```으로 불러왔다.
- 주의해야할 점은 문제에서도 언급되었듯이 하루 동안 직원은 두 번 이상 출입할 수 있다는 점이다. 이 점을 고려하여 사무실에서 보낸 시간을 ```SUM``` 함수로 두 번 이상 출입했을 때에도 ```total_time```에 더해질 수 있도록 했다.
- EASY 😎
- [👉 문제 보러가기](https://leetcode.com/problems/find-total-time-spent-by-each-employee/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}