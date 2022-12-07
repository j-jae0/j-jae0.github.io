---
title:  "[리트코드 SQL] Day 2. Select & Order"
layout: single

categories: "Algorithm_SQL"
tags: ["CASE", "ORDER BY", "UPDATE", "SET", "DELETE", "JOIN", "WHERE"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL I : Day 2 Select & Order 3문제 풀이</small>

***

# <span class="half_HL">✔️ 1873. Calculate Special Bonus</span>

## (1) 코드 작성
```sql
SELECT EMPLOYEE_ID,
       CASE
         WHEN LEFT(NAME, 1) != 'M' AND EMPLOYEE_ID % 2 != 0 THEN SALARY ELSE 0
       END AS BONUS
FROM EMPLOYEES
ORDER BY EMPLOYEE_ID
```

## (2) 코드 리뷰 및 회고
- 문제는 이름이 'M'으로 시작하지 않고 ID가 홀수인 경우를 불러오는 것이다.
- 두 조건에 따라 ```SALARY``` 또는 ```0```을 출력해야하기 때문에 ```CASE``` 문을 사용했다.
- EASY 😎
- [👉 문제 보러가기](https://leetcode.com/problems/calculate-special-bonus/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">✔️ 627. Swap Salary</span>

## (1) 코드 작성
```sql
UPDATE SALARY
SET SEX = CASE WHEN SEX = 'm' THEN 'f' ELSE 'm' END
```

## (2) 코드 리뷰 및 회고
- 문제를 보면, ```UPDATE``` 문을 사용하고 ```SELECT``` 문을 사용하지 말라는 조건이 있다.
- 위 조건을 적용하기 위해 ```UPDATE ~ SET``` 문을 사용했다.
  - 그리고 ```SET```에 ```CASE```문을 추가하여 성별이 뒤집혀질 수 있도록 설정했다.
- [👉 문제 보러가기](https://leetcode.com/problems/swap-salary/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">✔️ 196. Delete Duplicate Emails</span>

## (1) 코드 작성
```sql
DELETE T1
FROM Person AS T1 
  INNER JOIN Person T2 ON T1.Email = T2.Email
WHERE T1.id > T2.id
```

## (2) 코드 리뷰 및 회고
- 문제를 보면, ```DELETE``` 문을 사용하고 ```SELECT``` 문을 사용하지 말라는 조건이 있다.
- 위 조건을 적용하기 위해 ```DELETE ~ FROM ~ WHERE``` 문을 사용했다.
  - **WHERE 절을 생략하면 해당 테이블에 저장된 모든 데이터가 삭제됨**
- [👉 문제 보러가기](https://leetcode.com/problems/delete-duplicate-emails/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}