---
title:  "[프로그래머스 SQL] Lv 4. 자동차 대여 기록 별 대여 금액 구하기"
layout: single

categories: "Algorithm_SQL"
tags: ["IF", "CASE", "JOIN", "DATEDIFF", "FLOOR"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - String, Date 문제</small>

***

# <span class="half_HL">✔️ 문제 설명</span>
```CAR_RENTAL_COMPANY_CAR``` 테이블과 ```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블과 ```CAR_RENTAL_COMPANY_DISCOUNT_PLAN``` 테이블에서 자동차 종류가 '트럭'인 자동차의 대여 기록에 대해서 대여 기록 별로 대여 금액(컬럼명: ```FEE```)을 구하여 대여 기록 ID와 대여 금액 리스트를 출력하는 SQL문을 작성해주세요. 결과는 대여 금액을 기준으로 내림차순 정렬하고, 대여 금액이 같은 경우 대여 기록 ID를 기준으로 내림차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/151141)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT TR.HISTORY_ID,
       IF (TR.DURATION_TYPE IS NULL, FLOOR(TR.RENTAL_DATE*TC.DAILY_FEE),
                                     FLOOR(TR.RENTAL_DATE*TC.DAILY_FEE*TD.DISCOUNT)) AS FEE
FROM (SELECT *, (DATEDIFF(END_DATE, START_DATE) + 1) AS RENTAL_DATE,
             CASE 
                WHEN (DATEDIFF(END_DATE, START_DATE) + 1) >= 90 THEN '90일 이상'
                WHEN (DATEDIFF(END_DATE, START_DATE) + 1) >= 30 THEN '30일 이상'
                WHEN (DATEDIFF(END_DATE, START_DATE) + 1) >= 7 THEN '7일 이상' ELSE NULL
             END AS DURATION_TYPE
      FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY) AS TR
  INNER JOIN CAR_RENTAL_COMPANY_CAR AS TC ON TR.CAR_ID = TC.CAR_ID
  LEFT JOIN (SELECT CAR_TYPE, DURATION_TYPE,
                    (1 - DISCOUNT_RATE*0.01) AS DISCOUNT
             FROM CAR_RENTAL_COMPANY_DISCOUNT_PLAN)
             AS TD ON TC.CAR_TYPE = TD.CAR_TYPE AND TR.DURATION_TYPE = TD.DURATION_TYPE
WHERE TC.CAR_TYPE = "트럭"
ORDER BY FEE DESC, HISTORY_ID DESC
```

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}