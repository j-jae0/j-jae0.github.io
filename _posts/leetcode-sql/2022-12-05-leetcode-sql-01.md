---
title:  "[리트코드 SQL] Day 1. Select"
layout: single

categories: "Algorithm_SQL"
tags: ["SELECT", "WHERE", "JOIN", "NULL"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL I : Day 1 Select 4문제 풀이</small>

***

# <span class="half_HL">✔️ 595. Big Countries</span>

| Column Name | Type    |
|:------------|:--------|
| name        | varchar |
| continent   | varchar |
| area        | int     |
| population  | int     |
| gdp         | int     |

**테이블명** : ```World```

name is the primary key column for this table.
Each row of this table gives information about the name of a country, the continent to which it belongs, its area, the population, and its GDP value.

A country is big if:
- it has an area of at least three million (i.e., 3000000 km2), or
- it has a population of at least twenty-five million (i.e., 25000000).

- Write an SQL query to report the name, population, and area of the big countries.
- Return the result table in any order.
- [👉 문제 보러가기](https://leetcode.com/problems/big-countries/)


## (1) 코드 작성
```sql
SELECT NAME, POPULATION, AREA
FROM WORLD
WHERE AREA >= 3000000 OR POPULATION >= 25000000
```

## (2) 코드 리뷰 및 회고
- 면적이 최소 300만, 인구가 최소 2500만명인 조건을 추가하기 위해 ```WHERE``` 절을 사용했다.
- 두 조건중 하나만 만족해도 되기 때문에 ```OR```로 조건식을 연결했다.
- EASY 😎


<br>

# <span class="half_HL">✔️ 1757. Recyclable and Low Fat Products</span>

| Column Name | Type    |
|:------------|:--------|
| product_id  | int     |
| low_fats    | enum    |
| recyclable  | enum    |

**테이블명** : ```Products```

product_id is the primary key for this table.
low_fats is an ENUM of type ('Y', 'N') where 'Y' means this product is low fat and 'N' means it is not.
recyclable is an ENUM of types ('Y', 'N') where 'Y' means this product is recyclable and 'N' means it is not.

- Write an SQL query to find the ids of products that are both low fat and recyclable.
- Return the result table in any order.
- [👉 문제 보러가기](https://leetcode.com/problems/recyclable-and-low-fat-products/)

## (1) 코드 작성
```sql
SELECT PRODUCT_ID
FROM PRODUCTS
WHERE LOW_FATS = 'Y' AND RECYCLABLE = 'Y'
```

## (2) 코드 리뷰 및 회고
- 제품이 저지방, 재활용 가능한 제품을 출력하기 위해 ```WHERE``` 절을 사용했다.
- 두 조건 모두 만족해야하기 때문에 ```AND``` 연산자로 두 조건을 연결했다.
- EASY 😎

<br>

# <span class="half_HL">✔️ 584. Find Customer Referee</span>

| Column Name | Type    |
|:------------|:--------|
| id          | int     |
| name        | varchar |
| referee_id  | int     |

**테이블명** : ```Customer```

id is the primary key column for this table.
Each row of this table indicates the id of a customer, their name, and the id of the customer who referred them.

- Write an SQL query to report the names of the customer that are not referred by the customer with ```id = 2```.
- Return the result table in any order.
- [👉 문제 보러가기](https://leetcode.com/problems/find-customer-referee/)

## (1) 코드 작성
```sql
SELECT NAME
FROM CUSTOMER
WHERE REFEREE_ID != 2 OR REFEREE_ID IS NULL
```

## (2) 코드 리뷰 및 회고
- 추천한 고객이 2가 아닌 경우를 출력하기 위해 2가 아니라는 조건을 작성했다.
- ```WHERE REFEREE_ID != 2``` 만 작성하니 NULL 값을 포함하는 데이터가 출력되지 않았다.
  - NULL 값을 포함하는 요소는 WHERE 절안의 조건식에 해당하지 않아도 제외 당하는 것 같다.
  - 이러한 이유로 ```WHERE``` 절에 ```REFEREE_ID IS NULL``` 조건식을 추가했다.
- 이 부분을 잘 기억해두어야할 것같다.(조건식, NULL 제외)
- EASY 😎

<br>

# <span class="half_HL">✔️ 183. Customers Who Never Order</span>

| Column Name | Type    |
|:------------|:--------|
| id          | int     |
| name        | varchar |

**테이블명** : ```Customers```

id is the primary key column for this table.
Each row of this table indicates the ID and name of a customer.


| Column Name | Type |
|:------------|:-----|
| id          | int  |
| customerId  | int  |

**테이블명** : ```Orders```

id is the primary key column for this table.
customerId is a foreign key of the ID from the Customers table.
Each row of this table indicates the ID of an order and the ID of the customer who ordered it.

- Write an SQL query to report all customers who never order anything.
- Return the result table in any order.
- [👉 문제 보러가기](https://leetcode.com/problems/customers-who-never-order/)

## (1) 코드 작성
```sql
SELECT C.NAME AS CUSTOMERS
FROM CUSTOMERS AS C
  LEFT JOIN ORDERS AS O ON C.ID = O.CUSTOMERID
WHERE O.ID IS NULL
```

## (2) 코드 리뷰 및 회고
- **목표** : 아무것도 주문하지 않은 고객 정보를 출력한다.
- 고객 데이터(고객 아이디, 고객명)과 주문 데이터(주문 번호, 고객 아이디)를 고객 아이디를 기준으로 ```JOIN``` 한다.
- 이때 주문을 하지 않은 고객 데이터를 출력하기 위해 고객은 모두 출력될 수 있도록 한다. 즉 ```LEFT JOIN```을 사용했다.
- 주문하지 않는 고객 정보 출력을 위해 주문 번호가 NULL인 조건식을 추가했다.
- EASY 😎

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}