---
title:  "[프로그래머스 SQL] Lv 1. 특정 옵션이 포함된 자동차 리스트 구하기"
layout: single

categories: "Algorithm_SQL"
tags: ["LIKE"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - String, Date 문제</small>

***

# <span class="half_HL">✔️ 문제 설명</span>
다음은 어느 자동차 대여 회사에서 대여중인 자동차들의 정보를 담은 ```CAR_RENTAL_COMPANY_CAR``` 테이블입니다. ```CAR_RENTAL_COMPANY_CAR``` 테이블은 아래와 같은 구조로 되어있으며, ```CAR_ID```, ```CAR_TYPE```, ```DAILY_FEE```, ```OPTIONS``` 는 각각 자동차 ID, 자동차 종류, 일일 대여 요금(원), 자동차 옵션 리스트를 나타냅니다.

|Column name|	Type|	Nullable|
|:----------|:------|:----------|
|CAR_ID|	INTEGER|	FALSE|
|CAR_TYPE	|VARCHAR(255)|	FALSE|
|DAILY_FEE|	INTEGER|	FALSE|
|OPTIONS	|VARCHAR(255)	|FALSE|

자동차 종류는 '세단', 'SUV', '승합차', '트럭', '리무진' 이 있습니다. 자동차 옵션 리스트는 콤마(',')로 구분된 키워드 리스트(옵션 리스트 값 예시: '열선시트', '스마트키', '주차감지센서')로 되어있으며, 키워드 종류는 '주차감지센서', '스마트키', '네비게이션', '통풍시트', '열선시트', '후방카메라', '가죽시트' 가 있습니다.

## 문제
```CAR_RENTAL_COMPANY_CAR``` 테이블에서 '네비게이션' 옵션이 포함된 자동차 리스트를 출력하는 SQL문을 작성해주세요. 결과는 자동차 ID를 기준으로 내림차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/157343)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT *
FROM CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS LIKE "%네비게이션%"
ORDER BY CAR_ID DESC
```

## (2) 코드 리뷰 및 회고
- 테이블에서 옵션 컬럼을 보면 '네비게이션, 열선시트, ...' 와 같이 여러 옵션들이 하나의 데이터로 합쳐져있다.
- 그래서 여러 옵션들 중 '네비게이션'이 포함된 자동차 리스트를 출력하기 위해 WHERE 문에 조건문을 작성했다.
- EASY 😎

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}