---
title:  "[프로그래머스 SQL] Lv 4. 특정 기간동안 대여 가능한 자동차들의 대여비용 구하기"
layout: single

categories: "Algorithm_SQL"
tags: ["TRUNCATE", "REGEXP", "NOT IN", "HAVING", "DATE_FORMAT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - JOIN 문제</small>

***

# <span class="half_HL">✔️ 문제 설명</span>
다음은 어느 자동차 대여 회사에서 대여 중인 자동차들의 정보를 담은 ```CAR_RENTAL_COMPANY_CAR``` 테이블과 자동차 대여 기록 정보를 담은 ```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블과 자동차 종류 별 대여 기간 종류 별 할인 정책 정보를 담은 ```CAR_RENTAL_COMPANY_DISCOUNT_PLAN``` 테이블 입니다.

```CAR_RENTAL_COMPANY_CAR``` 테이블은 아래와 같은 구조로 되어있으며, ```CAR_ID```, ```CAR_TYPE```, ```DAILY_FEE```, ```OPTIONS``` 는 각각 자동차 ID, 자동차 종류, 일일 대여 요금(원), 자동차 옵션 리스트를 나타냅니다.

|Column name|	Type	|Nullable|
|:--------------|:---|:---------|
|CAR_ID|	INTEGER	|FALSE|
|CAR_TYPE|	VARCHAR(255)|	FALSE|
|DAILY_FEE|	INTEGER	|FALSE|
|OPTIONS|	VARCHAR(255)|	FALSE|

자동차 종류는 '세단', 'SUV', '승합차', '트럭', '리무진' 이 있습니다. 자동차 옵션 리스트는 콤마(',')로 구분된 키워드 리스트(예: ''열선시트,스마트키,주차감지센서'')로 되어있으며, 키워드 종류는 '주차감지센서', '스마트키', '네비게이션', '통풍시트', '열선시트', '후방카메라', '가죽시트' 가 있습니다.

```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블은 아래와 같은 구조로 되어있으며, ```HISTORY_ID```, ```CAR_ID```, ```START_DATE```, ```END_DATE``` 는 각각 자동차 대여 기록 ID, 자동차 ID, 대여 시작일, 대여 종료일을 나타냅니다.

|Column name|	Type|	Nullable|
|:--------------|:---|:---------|
|HISTORY_ID	|INTEGER|	FALSE|
|CAR_ID	|INTEGER|	FALSE|
|START_DATE	|DATE	|FALSE|
|END_DATE	|DATE	|FALSE|

```CAR_RENTAL_COMPANY_DISCOUNT_PLAN``` 테이블은 아래와 같은 구조로 되어있으며, ```PLAN_ID```, ```CAR_TYPE```, ```DUTAION_TYPE```, ```DISCOUNT_RATE``` 는 각각 요금 할인 정책 ID, 자동차 종류, 대여 기간 종류, 할인율(%)을 나타냅니다.

|Column name	|Type|	Nullable|
|:--------------|:---|:---------|
|PLAN_ID|	INTEGER|	FALSE|
|CAR_TYPE	|VARCHAR(255)|	FALSE|
|DURAION_TYPE|	VARCHAR(255)|	FALSE|
|DISCOUNT_RATE|	INTEGER	|FALSE|

할인율이 적용되는 대여 기간 종류로는 '7일 이상' (대여 기간이 7일 이상 30일 미만인 경우), '30일 이상' (대여 기간이 30일 이상 90일 미만인 경우), '90일 이상' (대여 기간이 90일 이상인 경우) 이 있습니다. 대여 기간이 7일 미만인 경우 할인정책이 없습니다.

## 문제
```CAR_RENTAL_COMPANY_CAR``` 테이블과 ```CAR_RENTAL_COMPANY_RENTAL_HISTORY ```테이블과 ```CAR_RENTAL_COMPANY_DISCOUNT_PLAN``` 테이블에서 자동차 종류가 '세단' 또는 'SUV' 인 자동차 중 2022년 11월 1일부터 2022년 11월 30일까지 대여 가능하고 30일간의 대여 금액이 50만원 이상 200만원 미만인 자동차에 대해서 자동차 ID, 자동차 종류, 대여 금액(컬럼명: ```FEE```) 리스트를 출력하는 SQL문을 작성해주세요. 결과는 대여 금액을 기준으로 내림차순 정렬하고, 대여 금액이 같은 경우 자동차 종류를 기준으로 오름차순 정렬, 자동차 종류까지 같은 경우 자동차 ID를 기준으로 내림차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/157339)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT C.CAR_ID, C.CAR_TYPE, TRUNCATE(DAILY_FEE*30*(1-DISCOUNT_RATE*0.01), 0) AS FEE
FROM (SELECT CAR_ID, CAR_TYPE, DAILY_FEE 
      FROM CAR_RENTAL_COMPANY_CAR
      WHERE CAR_TYPE REGEXP '세단|SUV') AS C
INNER JOIN (SELECT CAR_TYPE, DISCOUNT_RATE
            FROM CAR_RENTAL_COMPANY_DISCOUNT_PLAN
            WHERE DURATION_TYPE = '30일 이상') AS D ON C.CAR_TYPE = D.CAR_TYPE
WHERE C.CAR_ID NOT IN (SELECT CAR_ID
                       FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
                       WHERE DATE_FORMAT(START_DATE, '%Y-%m-%d') < '2022-12-01' 
                         AND DATE_FORMAT(END_DATE, '%Y-%m-%d') > '2022-11-01')
HAVING FEE >= 500000 AND FEE < 2000000
ORDER BY FEE DESC, CAR_TYPE, CAR_ID DESC
```

## (2) 코드 리뷰 및 회고
**코드를 작성할 때 아래와 같은 슈도코드를 작성하였다.**
- 대여기간 조건을 만족하는 CAR_ID 
- 30일 대여시 할인율과 차 종류
- 차 종류별 데일리 요금
- 위 세 테이블을 합쳐서 차 종류별로 30일 대여시 FEE 출력

<u>서브쿼리를 너무 많이 생성해서 서브쿼리를 많이 생성하지 않는 방법으로 다시 코드를 작성해보는 연습을 해봐야겠다.</u>

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}