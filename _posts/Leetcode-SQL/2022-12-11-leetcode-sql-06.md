---
title:  "[리트코드 SQL] Day 5. Union"
layout: single

categories: "Algorithm_SQL"
tags: ["JOIN", "GROUP BY", "ORDER BY", "IS NULL", "COUNT", "DISTINCT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL I : Day 5 Union 3문제 풀이</small>

***

# <span class="half_HL">175. Combine Two Tables</span>

## (1) 코드 작성
```sql
SELECT P.FIRSTNAME, P.LASTNAME, A.CITY, A.STATE
FROM PERSON AS P
  LEFT JOIN ADDRESS AS A ON P.PERSONID = A.PERSONID
```

## (2) 코드 리뷰 및 회고
- 문제는 두 테이블을 사람 정보를 기준으로 결합하고 빈 값은 ```NULL```로 불러오는 것이다.
- 두 테이블을 ```LEFT JOIN```으로 ```ID```를 기준으로 결합하고 필요한 컬럼을 불러올 수 있도록 설정했다.
- EASY 😎
- [👉 문제 보러가기](https://leetcode.com/problems/combine-two-tables/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1581. Customer Who Visited but Did Not Make Any Transactions</span>

## (1) 코드 작성
```sql
SELECT V.CUSTOMER_ID, COUNT(*) AS COUNT_NO_TRANS
FROM VISITS AS V
  LEFT JOIN TRANSACTIONS AS T ON V.VISIT_ID = T.VISIT_ID
WHERE TRANSACTION_ID IS NULL
GROUP BY V.CUSTOMER_ID
ORDER BY COUNT_NO_TRANS DESC, V.CUSTOMER_ID
```

## (2) 코드 리뷰 및 회고
- 문제는 ```TRANSACTION``` 이용하지 않은 방문객들의 정보를 출력하는 것이다.
- ```LEFT JOIN```으로 방문객 정보를 다 불러오고 **TRANSACTION 정보가 빈 경우**가 출력되도록 조건문을 작성했다. 
- 그 후 고객 아이디를 기준으로 그룹화하고 ```COUNT``` 함수로 고객아이디별로 몇 번 TRANSACTION를 이용하지 않았는지 출력될 수 있도록 했다.
-  그리고 출력예시와 같게 만들기 위해 정렬 조건을 추가했다.
- EASY 😎
- [👉 문제 보러가기](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1148. Article Views I</span>

## (1) 코드 작성
```sql
SELECT DISTINCT AUTHOR_ID AS ID
FROM VIEWS
WHERE AUTHOR_ID = VIEWER_ID
ORDER BY ID
```

## (2) 코드 리뷰 및 회고
- 문제는 자신의 기사를 하나 이상 본 작성자의 정보를 출력하는 것이다.
- 즉, 저자 ID와 뷰어 ID가 같은 조건을 추가했다.
- 그리고 저자 아이디를 불러올 때 오름차순으로 정렬하고 ```DISTINCT```를 추가하여 중복된 값은 대표 1개만 나올 수 있도록 했다.
- EASY 😎
- [👉 문제 보러가기](https://leetcode.com/problems/article-views-i/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}