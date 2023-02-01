---
title:  "[프로그래머스 SQL] Lv 3. 대여 횟수가 많은 자동차들의 월별 대여 횟수 구하기"
layout: single

categories: "Algorithm_SQL"
tags: [""]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<br>

***

# <span class="half_HL">✔️ 문제 설명</span>
다음은 어느 자동차 대여 회사의 자동차 대여 기록 정보를 담은 ```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블입니다. ```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블은 아래와 같은 구조로 되어있으며, ```HISTORY_ID```, ```CAR_ID```, ```START_DATE```, ```END_DATE``` 는 각각 자동차 대여 기록 ID, 자동차 ID, 대여 시작일, 대여 종료일을 나타냅니다.

|Column name|	Type	|Nullable|
|:----------|:----------|:-------|
|HISTORY_ID|	INTEGER|	FALSE|
|CAR_ID|	INTEGER|	FALSE|
|START_DATE|	DATE|	FALSE|
|END_DATE|	DATE|	FALSE|

## 문제
```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블에서 대여 시작일을 기준으로 2022년 8월부터 2022년 10월까지 총 대여 횟수가 5회 이상인 자동차들에 대해서 해당 기간 동안의 월별 자동차 ID 별 총 대여 횟수(컬럼명: ```RECORDS```) 리스트를 출력하는 SQL문을 작성해주세요. 결과는 월을 기준으로 오름차순 정렬하고, 월이 같다면 자동차 ID를 기준으로 내림차순 정렬해주세요. 특정 월의 총 대여 횟수가 0인 경우에는 결과에서 제외해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/151139)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT MONTH(START_DATE) AS MONTH, CAR_ID, COUNT(*) AS RECORDS
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE CAR_ID IN (SELECT CAR_ID
                 FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
                 WHERE DATE_FORMAT(START_DATE, "%Y-%m") REGEXP "2022-08|2022-09|2022-10"
                 GROUP BY CAR_ID
                 HAVING COUNT(*) >= 5)
  AND DATE_FORMAT(START_DATE, "%Y-%m") REGEXP "2022-08|2022-09|2022-10"
GROUP BY MONTH, CAR_ID
ORDER BY MONTH, CAR_ID DESC
```

## (2) 코드 리뷰 및 회고
1. 2022년 8, 9, 10월까지 총 대여 횟수가 5회 이상인 자동차 ID를 가져오기 위해 WHERE문에 IN으로 조건에 맞는 자동차 ID를 불러왔다.
2. 그리고 대여 시작일이 2022년 8, 9, 10월인 조건을 추가한다.
3. 대여 월, 자동차ID로 그룹화하고 월별 자동차 ID별 대여 횟수를 출력할 수 있도록 COUNT 함수를 사용한다.

코드를 작성하면서 조금 더 간결하게 그리고 보기 좋게 작성할 수 있는 방법이 없을지 고민을 많이 했다.
정확히 어떤 데이터를 가져와야하는지, 그 데이터를 가져오기 위해선 어떤 순서로 불러와야할지를 먼저 고민해 보았다.

**➕ 추가로 알아볼 일**
- 다른 방법으로 데이터를 불러올 수 없는지 고민해 보기

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}