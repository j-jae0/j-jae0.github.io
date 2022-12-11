---
title:  "[리트코드 SQL] Day 4-1. Union & Select"
layout: single

categories: "Algorithm_SQL"
tags: ["JOIN", "WHERE", "IS NULL", "IS NOT NULL", "UNION"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL I : Day 4-1 Union & Select 2문제 풀이</small>

***

# <span class="half_HL">1965. Employees With Missing Information</span>

## (1) 코드 작성
```sql
(SELECT E.EMPLOYEE_ID
FROM EMPLOYEES AS E
  LEFT JOIN SALARIES AS S ON E.EMPLOYEE_ID = S.EMPLOYEE_ID
WHERE S.SALARY IS NULL

UNION

SELECT S.EMPLOYEE_ID
FROM EMPLOYEES AS E
  RIGHT JOIN SALARIES AS S ON E.EMPLOYEE_ID = S.EMPLOYEE_ID
WHERE E.NAME IS NULL)
ORDER BY EMPLOYEE_ID
```

## (2) 코드 리뷰 및 회고
- 문제는 정보가 누락된 직원 데이터를 출력하는 것이다.
- 두 테이블(```EMPLOYEES```, ```SALARIES```)를 **LEFT JOIN** / **RIGHT JOIN**하여 급여 정보가 누락된 경우와 이름 정보가 누락된 경우를 찾고 ```UNION```으로 붙여주었다.
- 마지막으로 직원 아이디를 기준으로 오름차순 정렬했다.
- [👉 문제 보러가기](https://leetcode.com/problems/employees-with-missing-information/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1795. Rearrange Products Table</span>

## (1) 코드 작성
```sql
SELECT PRODUCT_ID, 'STORE1' as STORE, STORE1 AS PRICE 
FROM PRODUCTS
WHERE STORE1 IS NOT NULL
UNION
SELECT PRODUCT_ID, 'STORE2' as STORE, STORE2 AS PRICE 
FROM PRODUCTS
WHERE STORE2 IS NOT NULL
UNION
SELECT PRODUCT_ID, 'STORE3' as STORE, STORE3 AS PRICE 
FROM PRODUCTS
WHERE STORE3 IS NOT NULL
```

## (2) 코드 리뷰 및 회고
- 문제는 컬럼으로 존재하는 정보를 행으로 전환하여 가져오는 것이다.
  - ```제품ID | 매장1 가격 | 매장2 가격 | 매장3 가격```
  - ```제품ID | 매장정보 | 가격```
- 위 조건을 만족하기 위해 ```SELECT-FROM-WHERE``` 구문을 3개 만들어 ```UNION```으로 묶어주었다.
- 매장 정보는 ```'STORE1'```과 같은 방식으로 일괄처리했고 컬럼명을 ```STORE```로 만들었다.
- [👉 문제 보러가기](https://leetcode.com/problems/rearrange-products-table/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}