---
title:  "[프로그래머스 SQL] Lv 2. 자동차 평균 대여 기간 구하기"
layout: single

categories: "Algorithm_SQL"
tags: ["DATEDIFF", "AVG", "ROUND", "HAVING"]

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
|:----------|:----------|:-------|
|HISTORY_ID|	INTEGER|	FALSE|
|CAR_ID|	INTEGER	|FALSE|
|START_DATE|	DATE|	FALSE|
|END_DATE|	DATE|	FALSE|

## 문제
```CAR_RENTAL_COMPANY_RENTAL_HISTORY``` 테이블에서 평균 대여 기간이 7일 이상인 자동차들의 자동차 ID와 평균 대여 기간(컬럼명: ```AVERAGE_DURATION```) 리스트를 출력하는 SQL문을 작성해주세요. 평균 대여 기간은 소수점 두번째 자리에서 반올림하고, 결과는 평균 대여 기간을 기준으로 내림차순 정렬해주시고, 평균 대여 기간이 같으면 자동차 ID를 기준으로 내림차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/157342)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT CAR_ID, ROUND(AVG(DATEDIFF(END_DATE, START_DATE) + 1), 1) AS AVERAGE_DURATION
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
GROUP BY CAR_ID
HAVING AVG(DATEDIFF(END_DATE, START_DATE) + 1) >= 7
ORDER BY AVERAGE_DURATION DESC, CAR_ID DESC
```

## (2) 코드 리뷰 및 회고
- 자동차 종류 별로 평균 대여 기간을 구하는 문제이다.
- 평균 대여 기간이 7일 이상인 케이스를 불러오기 위해 ```CAR_ID```를 기준으로 그룹화 한 뒤, ```HAVING``` 문에 조건을 넣었다.
- 그리고 대여 기간을 구하기 위해 날짜(DATE) 데이터의 차를 구할 수 있는 ```DATEDIFF``` 함수를 사용했다.
- 평균 값과 소수 둘째자리에서의 반올림을 위해 ```AVG```, ```ROUND``` 함수도 사용했다.
- **두 날짜(대여시작일, 대여종료일)의 차를 구하고 1을 더하는 이유는 대여 시작일 첫 날을 고려하기 위해서이다.**

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}