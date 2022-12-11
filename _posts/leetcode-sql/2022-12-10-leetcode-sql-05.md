---
title:  "[리트코드 SQL] Day 4-2. Union & Select"
layout: single

categories: "Algorithm_SQL"
tags: ["CASE", "IS NULL", "MAX", "WHERE"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL I : Day 4-2 Union & Select 2문제 풀이</small>

***

# <span class="half_HL">608. Tree Node</span>

## (1) 코드 작성
```sql
SELECT ID,
       CASE 
         WHEN P_ID IS NULL THEN 'Root'
         WHEN ID IN (SELECT DISTINCT P_ID FROM TREE) THEN 'Inner' ELSE 'Leaf'
       END AS TYPE
FROM TREE
```

## (2) 코드 리뷰 및 회고
- 
- [👉 문제 보러가기](https://leetcode.com/problems/tree-node/description/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">176. Second Highest Salary</span>

## (1) 코드 작성
```sql
SELECT MAX(SALARY) AS SecondHighestSalary
FROM EMPLOYEE
WHERE SALARY < (SELECT MAX(SALARY) FROM EMPLOYEE)
```

## (2) 코드 리뷰 및 회고
- 문제는 두 번째로 높은 급여를 출력하는 것이다.
- 테이블에서 가장 높은 급여 정보를 뺀 후, 그 다음으로 높은 급여(전체적으로 2번 째로 높은 급여) 정보를 가져오기 위해 ```WHERE``` 절을 사용했다.
- ```WHERE```절에 ```SELECT-FROM``` 문을 사용하여 가장 급여가 높은 경우를 제외했다.
- [👉 문제 보러가기](https://leetcode.com/problems/second-highest-salary/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}