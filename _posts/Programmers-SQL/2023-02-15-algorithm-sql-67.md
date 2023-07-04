---
title:  "[프로그래머스 SQL] Lv 3. 대여 기록이 존재하는 자동차 리스트 구하기"
layout: single

categories: "Algorithm_SQL"
tags: ["DISTINCT", "JOIN"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - String, Date 문제</small>

***

# <span class="half_HL">✔️ 문제 설명</span>
다음은 어느 자동차 대여 회사에서 대여 중인 자동차들의 정보를 담은 ```CAR_RENTAL_COMPANY_CAR``` 테이블과 자동차 대여 기록 정보를 담은 ```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블입니다. 

```CAR_RENTAL_COMPANY_CAR``` 테이블은 아래와 같은 구조로 되어있으며, ```CAR_ID```, ```CAR_TYPE```, ```DAILY_FEE```, ```OPTIONS``` 는 각각 자동차 ID, 자동차 종류, 일일 대여 요금(원), 자동차 옵션 리스트를 나타냅니다.

|Column name|	Type	|Nullable|
|:----------|:----------|:--------|
|CAR_ID	|INTEGER	|FALSE|
|CAR_TYPE|	VARCHAR(255)|	FALSE|
|DAILY_FEE	|INTEGER|	FALSE|
|OPTIONS|	VARCHAR(255)|	FALSE|

자동차 종류는 '세단', 'SUV', '승합차', '트럭', '리무진' 이 있습니다. 자동차 옵션 리스트는 콤마(',')로 구분된 키워드 리스트(예: '열선시트', '스마트키', '주차감지센서')로 되어있으며, 키워드 종류는 '주차감지센서', '스마트키', '네비게이션', '통풍시트', '열선시트', '후방카메라', '가죽시트' 가 있습니다.

```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블은 아래와 같은 구조로 되어있으며, ```HISTORY_ID```, ```CAR_ID```, ```START_DATE```, ```END_DATE``` 는 각각 자동차 대여 기록 ID, 자동차 ID, 대여 시작일, 대여 종료일을 나타냅니다.

|Column name|	Type|	Nullable|
|:----------|:------|:----------|
|HISTORY_ID|	INTEGER|	FALSE|
|CAR_ID|	INTEGER|	FALSE|
|START_DATE|	DATE|	FALSE|
|END_DATE|	DATE|	FALSE|

## 문제
```CAR_RENTAL_COMPANY_CAR``` 테이블과 ```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블에서 자동차 종류가 '세단'인 자동차들 중 10월에 대여를 시작한 기록이 있는 자동차 ID 리스트를 출력하는 SQL문을 작성해주세요. 자동차 ID 리스트는 중복이 없어야 하며, 자동차 ID를 기준으로 내림차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/157341)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT DISTINCT T1.CAR_ID
FROM (SELECT *
      FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
      WHERE MONTH(START_DATE) = "10") AS T1
INNER JOIN CAR_RENTAL_COMPANY_CAR AS T2 ON T1.CAR_ID = T2.CAR_ID
WHERE T2.CAR_TYPE = "세단"
ORDER BY T1.CAR_ID DESC
```

## (2) 코드 리뷰 및 회고
- 두 테이블을 결합할 때, ```INNER JOIN``` 으로 한 이유는 렌탈 기록 테이블에 존재하는 데이터만 불러오기 위해서이다.
- 렌탈 정보가 기록된 테이블을 불러올 때, 서브쿼리를 만들어 10월에 렌탈 기록이 있는 정보만 불러왔다.
- 두 테이블을 결합한 후, 차 종류가 세단인 데이터만 불러올 수 있도록 ```WHERE``` 문을 추가했다.
- 출력할 항목은 자동차 아이디를 중복제거하여 불러온다.
- 전체적인 흐름은 아래와 같다.
  - 대여 기록 테이블에서 10월에 대여기록이 있는 대여 ID, 자동차 ID, 대여 시작일, 대여 종료일을 불러온다.(```서브쿼리```)
  - 자동차 정보를 담은 테이블과 ```INNER JOIN```을 하여 자동차 ID별로 자동차 종류가 무엇인지를 알 수 있도록 한다.
  - 차 종류가 세단인 데이터만 불러온다.
  - 대여 기록 테이블을 중심으로 불러왔기 때문에 같은 자동차 ID를 가진 행이 많이 출력될 것이다.
  - 위 사항을 고려하여 ```DISTINCT``` 로 자동차 ID를 중복제거하여 불러온다.

<br>

## 🤔 THINK
나는 서브쿼리와 ```JOIN```을 통해 데이터를 출력했지만 또 다른 방법으로 불러온다면 대여 가능한 자동차 정보 테이블을 ```FROM```으로 불러오고, ```WHERE``` 문에 대여 시작일이 10일인 ```CAR_ID```를 포함한다는 조건과 자동차 종류가 세단인 조건을 ```AND``` 로 불러오는 것도 가능할 것이다.

<u>생각한 코드는 아래와 같고, 제출 후 채점하기를 했을 때 정답 sign이 떴다.</u>

```sql
SELECT CAR_ID
FROM CAR_RENTAL_COMPANY_CAR
WHERE CAR_TYPE = "세단" 
  AND CAR_ID IN (SELECT CAR_ID 
                 FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
                 WHERE MONTH(START_DATE) = "10")
ORDER BY CAR_ID DESC
```

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}