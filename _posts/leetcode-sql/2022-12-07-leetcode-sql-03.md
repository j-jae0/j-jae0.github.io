---
title:  "[리트코드 SQL] Day 3. String Processing Functions"
layout: single

categories: "Algorithm_SQL"
tags: ["UPPER", "LEFT", "LOWER", "RIGHT", "CONCAT", "COUNT", "DISTINCT", "GROUP_CONCAT", "LIKE"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL I : Day 3 String Processing Functions 3문제 풀이</small>

***

# <span class="half_HL">1667. Fix Names in a Table</span>

## (1) 코드 작성
```sql
SELECT USER_ID, CONCAT(UPPER(LEFT(NAME, 1)), LOWER(RIGHT(NAME, LENGTH(NAME)-1))) AS NAME
FROM USERS
ORDER BY USER_ID
```

## (2) 코드 리뷰 및 회고
- 문제는 이름을 첫 글자를 대문자, 나머지를 소문자로 변경하는 것이다.
  - 이 조건을 만족하기 위해 ```UPPER```, ```LEFT```, ```LOWER```, ```RIGHT``` 함수를 사용함
  - 두 경우를 결합하기 위해 ```CONCAT``` 함수를 사용
- ```UPPER```, ```LOWER```, ```LEFT```, ```RIGHT``` 함수는 알았으나 두 개를 묶는 방법을 몰라서 검색을 통해 배웠다.
  - ```CONCAT``` : <u>여러 문자열을 하나의 문자열로 합치는 함수</u>
- [👉 문제 보러가기](https://leetcode.com/problems/fix-names-in-a-table/description/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1484. Group Sold Products By The Date</span>

## (1) 코드 작성
```sql
SELECT SELL_DATE, COUNT(DISTINCT PRODUCT) AS NUM_SOLD
     , GROUP_CONCAT(DISTINCT PRODUCT) AS PRODUCTS
FROM ACTIVITIES
GROUP BY SELL_DATE
ORDER BY SELL_DATE
```

## (2) 코드 리뷰 및 회고
- 문제는 ```SELL_DATE```로 그룹화하여 상품 개수, 상품 리스트를 출력하는 것이다.
- 이때, 그룹화하여 상품을 출력하면 1개의 값만 출력하기 때문에 묶어줘야한다.
  - 이 조건을 만족시키기 위해 ```GROUP_CONCAT()``` 를 사용했다.
  - ```GROUP BY(DISTINCT 컬럼명)``` / ```GROUP BY(컬럼명 SEPARATOR '구분자')``` 등을 사용할 수 있음
  - 구분자 명령어를 사용하지 않으면 기본값으로 ','로 문자열이 구분됨
- ```DISTINCT``` 로 중복 시 하나의 값만 출력될 수 있도록 지정했다.
- 이 문제를 통해 ```GROUP_CONCAT```을 이용하면 특정 데이터들을 한 줄로 표현할 수 있음을 배웠다!
  - 오늘도 하나 배웠다 ! 발전! 🙋🏻‍♀️
- [👉 문제 보러가기](https://leetcode.com/problems/group-sold-products-by-the-date/description/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1527. Patients With a Condition</span>

## (1) 코드 작성
```sql
SELECT PATIENT_ID, PATIENT_NAME, CONDITIONS
FROM PATIENTS
WHERE CONDITIONS LIKE 'DIAB1%' OR CONDITIONS LIKE '% DIAB1%'
```

## (2) 코드 리뷰 및 회고
- 이번 문제는 제 1형 당뇨병 환자의 정보를 불러오는 것이다.
  - 이 조건을 만족하기 위해 DIAB1 를 접두사로 사용하는 경우를 추가했다.
  - ```WHERE CONDITIONS LIKE 'DIAB1%' OR CONDITIONS LIKE '%DIAB1%'``` 로 하면 오답처리됨
  - 이유는 문자열 중 맨 앞이거나, 'ACNE DIAB100' 처럼 공백 1칸과 함께 시작하는 경우만 해당
- EASY 😎
- [👉 문제 보러가기](https://leetcode.com/problems/patients-with-a-condition/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}