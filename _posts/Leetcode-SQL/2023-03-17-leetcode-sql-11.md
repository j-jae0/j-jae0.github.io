---
title:  "[리트코드 SQL] Day 10. Where"
layout: single

categories: "Algorithm_SQL"
tags: ["COUNT", "LEFT JOIN", "INNER JOIN"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL I : Day 10 Where 4문제 풀이</small>

***

# <span class="half_HL">182. Duplicate Emails</span>
모든 중복 이메일을 보고하는 SQL 쿼리를 작성하시오. 이메일 필드가 NULL이 아님이 보장됩니다.<br>
테이블: ```Person```

| Column Name    | Type     |
|:---------------|:---------|
| id             | int      |
| email          | varchar  |

## (1) 코드 작성
```sql
SELECT Email
FROM Person
GROUP BY email
HAVING COUNT(*) > 1
```

## (2) 코드 리뷰 및 회고
- 이메일이 같은 케이스를 불러오기 위해 email로 그룹화하고 ```COUNT``` 함수로 1개보다 큰 경우를 출력했다.
- EASY 😎
- [👉 문제 보러가기](https://leetcode.com/problems/duplicate-emails/submissions/917934434/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1050. Actors and Directors Who Cooperated At Least Three Times</span>
배우가 감독과 최소 세 번 협력한 쌍(actor_id, director_id)을 제공하는 보고서에 대한 SQL 쿼리를 작성하시오.<br>
테이블: ```ActorDirector```

| Column Name | Type    |
|:------------|:--------|
| actor_id    | int     |
| director_id | int     |
| timestamp   | int     |

## (1) 코드 작성
```sql
SELECT actor_id, director_id
FROM ActorDirector
GROUP BY actor_id, director_id
HAVING COUNT(*) >= 3
```

## (2) 코드 리뷰 및 회고
- 문제는 한 배우가 같은 감독과 세번 이상 함께 한 경우를 불러오는 것이다.
- 문제를 만족하기 위해 배우와 감독을 기준으로 그룹화하고 ```COUNT``` 함수로 3이상인 경우만 불러올 수 있도록 쿼리를 작성했다.
- [👉 문제 보러가기](https://leetcode.com/problems/actors-and-directors-who-cooperated-at-least-three-times/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1587. Bank Account Summary II</span>
잔액이 10000 이상인 사용자의 이름과 잔액을 보고하는 SQL 쿼리를 작성하시오. 계정 잔액은 해당 계정과 관련된 모든 거래 금액의 합계와 같습니다.<br>
테이블: ```Users```

| Column Name | Type    |
|:------------|:--------|
| account     | int     |
| name        | varchar |

테이블: ```Transactions```

| Column Name   | Type    |
|:--------------|:--------|
| trans_id      | int     |
| account       | int     |
| amount        | int     |
| transacted_on | date    |

## (1) 코드 작성
```sql
SELECT U.name, T.balance
FROM Users AS U
LEFT JOIN (SELECT account
                , SUM(amount) AS balance
           FROM Transactions
           GROUP BY account) AS T ON U.account = T.account
WHERE T.balance > 10000
```

## (2) 코드 리뷰 및 회고
- 문제는 유저별로 잔액이 10000보다 큰 경우만 출력하는 것이다.
- ```Transaction``` 테이블에서 account(계정)을 기준으로 그룹화하고 계정별로 잔액을 ```SUM``` 함수로 잔액을 출력한 것을 서브 쿼리로 불러오고 유저 테이블과 계정을 기준으로 ```JOIN``` 하였다.
  - 이때 조인은 ```INNER JOIN```을 사용해도 되지만 ```LEFT JOIN```을 써봤다.
- 그리고 잔액(balance)가 10000보다 큰 경우만 출력될 수 있도록 쿼리를 작성했다.
- EASY 😎
- [👉 문제 보러가기](https://leetcode.com/problems/bank-account-summary-ii/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1084. Sales Analysis III</span>
2019년 1분기에만 판매된 제품을 보고하는 SQL 쿼리를 작성하시오. 1분기는 2019-01-01과 2019-03-31 사이입니다.<br>
테이블: ```Product```

| Column Name  | Type    |
|:-------------|:--------|
| product_id   | int     |
| product_name | varchar |
| unit_price   | int     |

테이블: ```Product```

| Column Name  | Type    |
|:-------------|:--------|
| seller_id   | int     |
| product_id  | int     |
| buyer_id    | int     |
| sale_date   | date    |
| quantity    | int     |
| price       | int     |

## (1) 코드 작성
```sql
SELECT P.product_id, P.product_name
FROM Product AS P
INNER JOIN (SELECT S1.product_id
            FROM (SELECT product_id, COUNT(*) AS num_sales1
                  FROM Sales
                  GROUP BY product_id) AS S1
            LEFT JOIN (SELECT product_id, COUNT(*) AS num_sales2
                       FROM Sales
                       WHERE sale_date >= '2019-01-01' AND sale_date <= '2019-03-31'
                       GROUP BY product_id) AS S2 ON S1.product_id = S2.product_id
            WHERE S1.num_sales1 = S2.num_sales2) AS S ON P.product_id = S.product_id
```

## (2) 코드 리뷰 및 회고
- 이번 문제는 해결하는데 시간이 많이 소요되었다.
- 문제를 만족하는데 필요한 조건은 아래와 같다.
  - 1분기 내에 판매 내역이 존재해야한다.
  - 1분기를 벗어난 일자에서 판매 내역이 있다면 제외되어야 한다.
- 위 조건을 만족하기 위해 아래 순서로 쿼리를 작성했다.
  - 판매 테이블에서 상품을 기준으로 그룹화하여 판매횟수를 ```num_sales1```로 불러온다.(```S1```)
  - 판매 테이블에서 1분기때 판매된 케이스, 상품을 기준으로 그룹화하여 판매횟수를 ```num_sales2```로 불러온다.(```S2```)
  - ```S1```과 ```S2``` 테이블을 ```LEFT JOIN```으로 결합하고 ```num_sales1```과 ```num_sales2```가 같은 경우만 새로운 테이블(```S```)로 불러온다.
  -  그리고 상품 테이블과 ```S``` 테이블을 ```INNER JOIN```으로 붙여 1분기에만 판매된 상품id와 상품이름이 출력되도록 쿼리를 작성했다.
- ```num_sales1```, ```num_sales2```를 만든 이유는 1분기 내에서만 판매된 경우는 num_sales1과 num_sales2 값이 같을 것이기 때문이다.
- [👉 문제 보러가기](https://leetcode.com/problems/sales-analysis-iii/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}