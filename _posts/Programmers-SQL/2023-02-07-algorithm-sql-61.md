---
title:  "[프로그래머스 SQL] Lv 1. 평균 일일 대여 요금 구하기"
layout: single

categories: "Algorithm_SQL"
tags: ["AVG", "ROUND"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - SELECT 문제</small>

***

# <span class="half_HL">✔️ 문제 설명</span>
다음은 어느 자동차 대여 회사에서 대여중인 자동차들의 정보를 담은 ```CAR_RENTAL_COMPANY_CAR``` 테이블입니다. ```CAR_RENTAL_COMPANY_CAR``` 테이블은 아래와 같은 구조로 되어있으며, ```CAR_ID```, ```CAR_TYPE```, ```DAILY_FEE```, ```OPTIONS``` 는 각각 자동차 ID, 자동차 종류, 일일 대여 요금(원), 자동차 옵션 리스트를 나타냅니다.

|Column name|	Type	|Nullable|
|:----------|:----------|:-------|
|CAR_ID	|INTEGER|	FALSE|
|CAR_TYPE|	VARCHAR(255)|	FALSE|
|DAILY_FEE	|INTEGER|	FALSE|
|OPTIONS|	VARCHAR(255)|	FALSE|

자동차 종류는 '세단', 'SUV', '승합차', '트럭', '리무진' 이 있습니다. 자동차 옵션 리스트는 콤마(',')로 구분된 키워드 리스트(예: '열선시트', '스마트키', '주차감지센서')로 되어있으며, 키워드 종류는 '주차감지센서', '스마트키', '네비게이션', '통풍시트', '열선시트', '후방카메라', '가죽시트' 가 있습니다.

## 문제
```CAR_RENTAL_COMPANY_CAR``` 테이블에서 자동차 종류가 'SUV'인 자동차들의 평균 일일 대여 요금을 출력하는 SQL문을 작성해주세요. 이때 평균 일일 대여 요금은 소수 첫 번째 자리에서 반올림하고, 컬럼명은 ```AVERAGE_FEE``` 로 지정해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/151136)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT ROUND(AVG(DAILY_FEE)) AS AVERAGE_FEE
FROM CAR_RENTAL_COMPANY_CAR
WHERE CAR_TYPE = 'SUV'
```

## (2) 코드 리뷰 및 회고
- 자동차 종류가 'SUV'만 불러와 평균값을 구하기 위해 WHERE 문을 사용하여 SUV 차량 정보만 가져올 수 있도록 조건문을 추가했다.
- 그리고 일일 대여 요금을 ```AVG``` 함수와 ```ROUND``` 함수를 사용하여 평균값을 구했다.
  - ```ROUND```를 사용하면 소수 첫 째자리에서 반올림한 결과를 구할 수 있음

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}