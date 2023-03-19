---
title:  "[리트코드 SQL] Day 9. Control of Flow"
layout: single

categories: "Algorithm_SQL"
tags: [""]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"

published: false
---

<small>SQL I : Day 9 Control of Flow 3문제 풀이</small>

***

# <span class="half_HL">1393. Capital Gain/Loss</span>

## (1) 코드 작성
```sql
SELECT stock_name
     , SUM(price) AS capital_gain_loss
FROM (SELECT stock_name
           , IF(operation = 'Buy', -1*price, price) AS price
      FROM Stocks) AS S
GROUP BY stock_name
```

## (2) 코드 리뷰 및 회고
- 
- [👉 문제 보러가기](https://leetcode.com/problems/capital-gainloss/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1407. Top Travellers</span>

## (1) 코드 작성
```sql
SELECT U.name
     , IF(R.distance IS NULL, 0, R.distance) AS travelled_distance
FROM Users AS U
LEFT JOIN (SELECT user_id AS id
                 , SUM(distance) AS distance
            FROM Rides
            GROUP BY user_id) AS R ON R.id = U.id
ORDER BY travelled_distance DESC, name
```

## (2) 코드 리뷰 및 회고
- 
- [👉 문제 보러가기](https://leetcode.com/problems/top-travellers/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1158. Market Analysis I</span>

## (1) 코드 작성
```sql
SELECT U.user_id AS buyer_id
     , U.join_date
     , IF(O.orders_in_2019 IS NULL, 0, O.orders_in_2019) AS orders_in_2019
FROM Users AS U
LEFT JOIN (SELECT buyer_id AS user_id
                 , COUNT(*) AS orders_in_2019
            FROM Orders
            WHERE YEAR(order_date) = '2019'
            GROUP BY buyer_id) AS O ON U.user_id = O.user_id
```

## (2) 코드 리뷰 및 회고
- 
- [👉 문제 보러가기](https://leetcode.com/problems/market-analysis-i/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}