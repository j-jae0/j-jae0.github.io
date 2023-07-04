---
title:  "[프로그래머스 SQL] Lv 2. 자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기"
layout: single

categories: "Algorithm_SQL"
tags: ["GROUP BY", "COUNT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - GROUP BY 문제</small>

***

다음은 어느 자동차 대여 회사에서 대여중인 자동차들의 정보를 담은 ```CAR_RENTAL_COMPANY_CAR``` 테이블입니다. ```CAR_RENTAL_COMPANY_CAR``` 테이블은 아래와 같은 구조로 되어있으며, ```CAR_ID```, ```CAR_TYPE```, ```DAILY_FEE```, ```OPTIONS``` 는 각각 자동차 ID, 자동차 종류, 일일 대여 요금(원), 자동차 옵션 리스트를 나타냅니다.

|Column name|	Type	|Nullable|
|:----------|:----------|:-------|
|CAR_ID	|INTEGER|	FALSE|
|CAR_TYPE|	VARCHAR(255)|	FALSE|
|DAILY_FEE	|INTEGER|	FALSE|
|OPTIONS|	VARCHAR(255)|	FALSE|

자동차 종류는 '세단', 'SUV', '승합차', '트럭', '리무진' 이 있습니다. 자동차 옵션 리스트는 콤마(',')로 구분된 키워드 리스트(예: '열선시트', '스마트키', '주차감지센서')로 되어있으며, 키워드 종류는 '주차감지센서', '스마트키', '네비게이션', '통풍시트', '열선시트', '후방카메라', '가죽시트' 가 있습니다.

## 문제
```CAR_RENTAL_COMPANY_CAR``` 테이블에서 '통풍시트', '열선시트', '가죽시트' 중 하나 이상의 옵션이 포함된 자동차가 자동차 종류 별로 몇 대인지 출력하는 SQL문을 작성해주세요. 이때 자동차 수에 대한 컬럼명은 ```CARS```로 지정하고, 결과는 자동차 종류를 기준으로 오름차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/151137)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT CAR_TYPE, COUNT(CAR_ID) AS CARS
FROM CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS REGEXP "가죽시트|열선시트|통풍시트"
GROUP BY CAR_TYPE
ORDER BY CAR_TYPE
```

## (2) 코드 리뷰 및 회고
- 옵션이 '통풍시트', '가죽시트', '열선시트' 중 하나라도 포함된 데이터를 불러오기 위해 ```REGEXP```를 사용했다.
- 그리고 차 종류를 기준으로 그룹화 하고 자동차 개수를 불러오기 위해 ```CAR_ID```를 ```COUNT``` 집계함수를 사용했다.

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}