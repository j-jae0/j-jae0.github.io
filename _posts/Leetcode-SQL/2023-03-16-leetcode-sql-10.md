---
title:  "[리트코드 SQL] Day 9. Control of Flow"
layout: single

categories: "Algorithm_SQL"
tags: ["SUM", "IF", "LEFT JOIN"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL I : Day 9 Control of Flow 3문제 풀이</small>

***

# <span class="half_HL">1393. Capital Gain/Loss</span>
각 주식의 자본 이득/손실을 보고하는 SQL 쿼리를 작성하십시오.
주식의 자본 이득/손실은 주식을 한 번 또는 여러 번 매매한 후의 총 이득 또는 손실입니다.<br>
테이블: ```Stocks```

| Column Name    | Type     |
|:---------------|:---------|
| stock_name    | varchar |
| operation     | enum    |
| operation_day | int     |
| price         | int     |

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
- ```Stocks``` 테이블에는 ```operation```(Buy/Sell)별로 주식 금액이 포함되어있다.
- 주식의 자본 이득 및 손실을 불러오기 위해 Buy일 때 Price는 - 값, Sell일 때 Price를 +로 불러와야 한다.
- ```FROM```으로 테이블을 불러올 때 서브쿼리를 만들고 IF문을 통해 price를 operation 값에 따라 - 또는 +로 처리하여 불러왔다.
- 불러온 테이블에서 ```stock_name```으로 그룹화하고 price를 ```SUM``` 함수로 이득 또는 손실 정도를 ```capital_gain_loss``` 컬럼으로 불러왔다.
- price가 -라면 손실, +라면 이득이다.
- [👉 문제 보러가기](https://leetcode.com/problems/capital-gainloss/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1407. Top Travellers</span>
각 사용자가 이동한 거리를 보고하는 SQL 쿼리를 작성하시오.

travelled_distance로 정렬된 결과 테이블을 내림차순으로 반환하고, 둘 이상의 사용자가 동일한 거리를 이동한 경우 이름별로 오름차순으로 정렬합니다.<br>
테이블: ```Users```

| Column Name    | Type     |
|:---------------|:---------|
| id            | int     |
| name          | varchar |

테이블: ```Rides```

| Column Name    | Type     |
|:---------------|:---------|
| id            | int     |
| user_id       | int     |
| distance      | int     |

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
- 유저는 Users 테이블에는 있지만 Rides에는 없을 수 있다는 점을 고려하여 ```IF``` 함수를 사용해 Ride 한 거리가 없다면(```IS NULL```) 0을 출력할 수 있도록 했다.
- [👉 문제 보러가기](https://leetcode.com/problems/top-travellers/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1158. Market Analysis I</span>
SQL 쿼리를 작성하여 각 사용자, 가입 날짜 및 2019년 구매자로 만든 주문 수를 찾으시오.<br>
테이블: ```Users```

| Column Name    | Type    |
|:---------------|:--------|
| user_id        | int     |
| join_date      | date    |
| favorite_brand | varchar |

테이블: ```Orders```

| Column Name   | Type    |
|:--------------|:--------|
| order_id      | int     |
| order_date    | date    |
| item_id       | int     |
| buyer_id      | int     |
| seller_id     | int     |

테이블: ```Items```

| Column Name   | Type    |
|:--------------|:--------|
| item_id       | int     |
| item_brand    | varchar |

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
- 문제는 2019년도에 구매이력이 있는 고객 id와 고객의 가입일, 2019년도의 주문 횟수를 출력하는 것이다.
- 문제를 만족하기 위해 주문 테이블에서 연도를 2019인 경우만 불러오고 고객별로 그룹화하여 2019년도의 주문 건수를 ```COUNT``` 함수로 불러왔다.(서브쿼리)
- 그리고 ```Users``` 테이블에는 있지만 2019년도에 주문이력이 없는 고객이 있을 경우를 대비하여 ```LEFT JOIN```으로 서브쿼리를 붙어주고 만약 2019년도에 주문 이력이 없는 고객(NULL)일 땐 0으로 불러올 수 있도록 ```IF``` 함수를 사용했다.
- [👉 문제 보러가기](https://leetcode.com/problems/market-analysis-i/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}