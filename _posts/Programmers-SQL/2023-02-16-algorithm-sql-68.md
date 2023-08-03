---
title:  "[프로그래머스 SQL] Lv 3. 자동차 대여 기록에서 대여중 / 대여 가능 여부 구분하기"
layout: single

categories: "Algorithm_SQL"
tags: ["CASE", "DATE_FORMAT", "MAX", "GROUP BY"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - GROUP BY 문제</small>

***

# <span class="half_HL">✔️ 문제 설명</span>
다음은 어느 자동차 대여 회사의 자동차 대여 기록 정보를 담은 ```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블입니다. ```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블은 아래와 같은 구조로 되어있으며, ```HISTORY_ID```, ```CAR_ID```, ```START_DATE```, ```END_DATE``` 는 각각 자동차 대여 기록 ID, 자동차 ID, 대여 시작일, 대여 종료일을 나타냅니다.

|Column name|	Type	|Nullable|
|:----------|:----------|:-------|
|HISTORY_ID|	INTEGER|	FALSE|
|CAR_ID|	INTEGER	|FALSE|
|START_DATE|	DATE|	FALSE|
|END_DATE|	DATE|	FALSE|

## 문제
```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블에서 2022년 10월 16일에 대여 중인 자동차인 경우 '대여중' 이라고 표시하고, 대여 중이지 않은 자동차인 경우 '대여 가능'을 표시하는 컬럼(컬럼명: ```AVAILABILITY```)을 추가하여 자동차 ID와 ```AVAILABILITY``` 리스트를 출력하는 SQL문을 작성해주세요. 이때 반납 날짜가 2022년 10월 16일인 경우에도 '대여중'으로 표시해주시고 결과는 자동차 ID를 기준으로 내림차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/157340)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT CAR_ID,
       CASE
         WHEN DATE_FORMAT(MAX(END_DATE), "%Y-%m-%d") >= "2022-10-16" THEN "대여중" ELSE "대여 가능"
       END AS AVAILABILITY
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE DATE_FORMAT(START_DATE, "%Y-%m-%d") <= "2022-10-16"
GROUP BY CAR_ID
ORDER BY CAR_ID DESC
```

## (2) 코드 리뷰 및 회고
- 문제는 2022년 10월 26일 시점에 자동차 ID 별로 대여 여부를 출력하는 것이다.
- WHERE 문을 사용하여 대여 시작일이 2022년 10월 26일 이후인 건은 출력되지 않도록 했다.
- 자동차 ID로 그룹화 하고, 대여 종료일의 최댓값이 2022년 10월 16일 이상인 경우를 대여 중으로 표기하고 그 외의 케이스를 대여 가능으로 출력될 수 있도록 CASE 문을 작성했다. 
- 출력할 항목이 '대여중' 또는 '대여 가능'이라는 점에서 IF 문을 사용해도 되지만 CASE 문을 사용해서 작성해 보고 싶었다.

<u>IF 문을 사용하여 AVAILABILITY 컬럼을 출력할 땐 아래와 같은 코드를 작성하면 된다.</u>

```sql
SELECT CAR_ID,
       IF (DATE_FORMAT(MAX(END_DATE), "%Y-%m-%d") >= "2022-10-16", "대여중", "대여 가능") AS AVAILABILITY
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE DATE_FORMAT(START_DATE, "%Y-%m-%d") <= "2022-10-16"
GROUP BY CAR_ID
ORDER BY CAR_ID DESC
```

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}