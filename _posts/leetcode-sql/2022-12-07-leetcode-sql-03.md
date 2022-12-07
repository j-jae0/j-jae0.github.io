---
title:  "[리트코드 SQL] Day 3. String Processing Functions"
layout: single

categories: "Algorithm_SQL"
tags: [""]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"

published: false
---

<small>SQL I : Day 3 String Processing Functions 3문제 풀이</small>

***

# <span class="half_HL">✔️ 1667. Fix Names in a Table</span>

## (1) 코드 작성
```sql
SELECT USER_ID, CONCAT(UPPER(LEFT(NAME, 1)), LOWER(RIGHT(NAME, LENGTH(NAME)-1))) AS NAME
FROM USERS
ORDER BY USER_ID
```

## (2) 코드 리뷰 및 회고
- 
- EASY 😎
- [👉 문제 보러가기](https://leetcode.com/problems/fix-names-in-a-table/description/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">✔️ 1484. Group Sold Products By The Date</span>

## (1) 코드 작성
```sql
SELECT SELL_DATE, COUNT(DISTINCT PRODUCT) AS NUM_SOLD
     , GROUP_CONCAT(DISTINCT PRODUCT) AS PRODUCTS
FROM ACTIVITIES
GROUP BY SELL_DATE
ORDER BY SELL_DATE
```

## (2) 코드 리뷰 및 회고
- 
- [👉 문제 보러가기](https://leetcode.com/problems/group-sold-products-by-the-date/description/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">✔️ 1527. Patients With a Condition</span>

## (1) 코드 작성
```sql
SELECT PATIENT_ID, PATIENT_NAME, CONDITIONS
FROM PATIENTS
WHERE CONDITIONS LIKE 'DIAB1%' OR CONDITIONS LIKE '% DIAB1%'
```

## (2) 코드 리뷰 및 회고
- 
- [👉 문제 보러가기](https://leetcode.com/problems/patients-with-a-condition/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}