---
title:  "[프로그래머스 SQL] Lv 1. 자동차 대여 기록에서 장기／단기 대여 구분하기"
layout: single

categories: "Algorithm_SQL"
tags: ["DATE_FORMAT", "CASE"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - String, Date 문제</small>

***

# <span class="half_HL">✔️ 문제 설명</span>
다음은 어느 자동차 대여 회사의 자동차 대여 기록 정보를 담은 ```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블입니다. ```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블은 아래와 같은 구조로 되어있으며, ```HISTORY_ID```, ```CAR_ID```, ```START_DATE```, ```END_DATE``` 는 각각 자동차 대여 기록 ID, 자동차 ID, 대여 시작일, 대여 종료일을 나타냅니다.

|Column name|	Type	|Nullable|
|:----------|:----------|:--------|
|HISTORY_ID|	INTEGER|	FALSE|
|CAR_ID|	INTEGER	|FALSE|
|START_DATE	|DATE|	FALSE|
|END_DATE|	DATE	|FALSE|

## 문제
```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블에서 대여 시작일이 2022년 9월에 속하는 대여 기록에 대해서 대여 기간이 30일 이상이면 '장기 대여' 그렇지 않으면 '단기 대여' 로 표시하는 컬럼(컬럼명: ```RENT_TYPE```)을 추가하여 대여기록을 출력하는 SQL문을 작성해주세요. 결과는 대여 기록 ID를 기준으로 내림차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/151138)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT HISTORY_ID, CAR_ID, 
       DATE_FORMAT(START_DATE, "%Y-%m-%d") AS START_DATE, 
       DATE_FORMAT(END_DATE, "%Y-%m-%d") AS END_DATE,
       CASE 
         WHEN DATEDIFF(END_DATE, START_DATE) + 1 < 30 THEN "단기 대여" ELSE "장기 대여" 
       END AS RENT_TYPE 
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE DATE_FORMAT(START_DATE, "%Y-%m") = "2022-09"
ORDER BY HISTORY_ID DESC
```

## (2) 코드 리뷰 및 회고
- 대여 기간을 기준으로 단기 대여, 장기 대여로 분류하기 위해 ```CASE``` 문을 사용했다. 
  - ```IF``` 문을 사용해도 되지만 ```CASE``` 문을 사용해서 적고 싶었음
- 단기와 장기를 나누는 기준은 대여 종료일에서 대여 시작일을 빼기 위해 ```DATEDIFF``` 함수를 사용했다.
  - **1을 더한 이유는 첫째날을 고려해주기 위해서이다.**

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}