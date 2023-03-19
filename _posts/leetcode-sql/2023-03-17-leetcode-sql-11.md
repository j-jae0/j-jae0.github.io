---
title:  "[리트코드 SQL] Day 10. Where"
layout: single

categories: "Algorithm_SQL"
tags: [""]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"

published: false
---

<small>SQL I : Day 10 Where 4문제 풀이</small>

***

# <span class="half_HL">182. Duplicate Emails
</span>

## (1) 코드 작성
```sql
SELECT Email
FROM Person
GROUP BY email
HAVING COUNT(*) > 1
```

## (2) 코드 리뷰 및 회고
- 
- [👉 문제 보러가기](https://leetcode.com/problems/duplicate-emails/submissions/917934434/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1050. Actors and Directors Who Cooperated At Least Three Times</span>

## (1) 코드 작성
```sql
SELECT actor_id, director_id
FROM ActorDirector
GROUP BY actor_id, director_id
HAVING COUNT(*) >= 3
```

## (2) 코드 리뷰 및 회고
- 
- [👉 문제 보러가기](https://leetcode.com/problems/actors-and-directors-who-cooperated-at-least-three-times/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1587. Bank Account Summary II</span>

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
- 
- [👉 문제 보러가기](https://leetcode.com/problems/bank-account-summary-ii/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1084. Sales Analysis III</span>

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
- 
- [👉 문제 보러가기](https://leetcode.com/problems/sales-analysis-iii/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}