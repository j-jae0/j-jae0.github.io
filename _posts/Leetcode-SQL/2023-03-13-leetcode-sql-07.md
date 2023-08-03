---
title:  "[리트코드 SQL] Day 6. Union"
layout: single

categories: "Algorithm_SQL"
tags: ["DATEDIFF", "JOIN", "NOT IN"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL I : Day 6 Union 2문제 풀이</small>

***

# <span class="half_HL">197. Rising Temperature</span>
이전 날짜(어제)에 비해 온도가 높은 모든 날짜의 Id를 찾는 SQL 쿼리를 작성하십시오.<br>
테이블(```Weather```)은 아래와 같다.

| Column Name | Type |
|:------------|:-----|
|id | int |
|recordDate | date |
|temperature | int |

## (1) 코드 작성
```sql
SELECT t1.id 
FROM weather AS t1, weather AS t2
WHERE t1.temperature > t2.temperature
  AND DATEDIFF(t1.recordDate, t2.recordDate) = 1
```

## (2) 코드 리뷰 및 회고
- 문제를 만족하기 위한 조건을 다음과 같다.
  - 비교 대상은 날짜를 기준으로 하루 차이가 난다.
  - 하루를 기준으로 다음 날짜의 온도가 더 높다.
- 두 조건을 만족하기 위해 같은 테이블 ```Weather``` 을 두 개 불러온다.
- 그리고 ```WHERE``` 문으로 첫 번째 테이블(```t1```)에서의 날짜와 두 번째 테이블(```t2```)에서의 날짜 차를 구하기 위해 ```DATEDIFF``` 함수를 사용했고 t1에서의 날짜가 t2에서의 날짜보다 1 큰 경우를 조건식으로 넣었다.
- 마지막으로 t1(다음날)의 온도가 더 크다는 조건식을 넣어 마무리했다.
- 이번 문제를 풀면서 ```FROM```에 ```,```로 두 테이블을 불러올 수 있다는 것을 알았다.
- [👉 문제 보러가기](https://leetcode.com/problems/rising-temperature/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">607. Sales Person</span>
이름이 "RED"인 회사와 관련된 주문이 없는 모든 영업 사원의 이름을 보고하는 SQL 쿼리를 작성하십시오.<br>
테이블: ```SalesPerson```

| Column Name | Type |
|:------------|:-----|
| sales_id | int |
| name | varchar |
| salary | int |
| commission_rate | int |
| hire_date | date |

테이블: ```Company```

| Column Name | Type    |
|:------------|:--------|
| com_id      | int     |
| name        | varchar |
| city        | varchar |

테이블: ```Orders```

| Column Name | Type |
|:------------|:-----|
| order_id    | int  |
| order_date  | date |
| com_id      | int  |
| sales_id    | int  |
| amount      | int  |

## (1) 코드 작성
```sql
SELECT name
FROM SalesPerson
WHERE sales_id NOT IN(SELECT sales_id 
                      FROM Orders AS O 
                      INNER JOIN Company AS C on O.com_id = C.com_id
                      WHERE C.name = 'RED')
```

## (2) 코드 리뷰 및 회고
- Red와 관련없는 영업사원의 이름을 불러오기 위해 ```WHERE``` 문과 ```NOT IN``` 함수를 사용했다.
- 주문 테이블과 회사 정보가 담긴 테이블을 회사 id를 기준으로 ```JOIN```하고 Red 회사에 주문건이 있는 영업 사원의 id를 불러오는 서브 쿼리를 작성한 다음 ```NOT IN``` 함수로 서브쿼리로 불러온 Red와 관련된 영업사원 아이디 리스트에 없는 영업사원만 불러오도록 조건식을 작성했다.
- [👉 문제 보러가기](https://leetcode.com/problems/sales-person/submissions/917395313/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}