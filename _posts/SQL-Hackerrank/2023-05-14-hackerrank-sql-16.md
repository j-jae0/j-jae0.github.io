---
title:  "[해커랭크 SQL] Aggregation 문제풀이 (5)"
layout: single

categories: "Algorithm_SQL"
tags: ["ROUND", "AVG", "ROW_NUMBER", "OVER", "CEIL", "FLOOR", "COUNT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 MEDIUM 1 문제 풀이</small>

***

# 📍 테이블 정보
The **STATION** table is described as follows:

| Field | Type |
|:-------|:-----|
| ID | NUMBER |
| CITY | VARCHAR2(21) |
| STATE | VARCHAR2(2) |
| LAT_N | NUMBER |
| LONG_W | NUMBER |

<small>cf. where LAT_N is the northern latitude and LONG_W is the western longitude.</small>

<br>

# 1. Weather Observation Station 20
A median is defined as a number separating the higher half of a data set from the lower half. Query the median of the Northern Latitudes (LAT_N) from STATION and round your answer to 4 decimal places.<br>
[Weather Observation Station 20 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-20/problem?isFullScreen=true)

## (1) 문제 이해

## (2) 코드 작성
```sql
SELECT ROUND(AVG(LAT_N), 4)
FROM (SELECT LAT_N
           , ROW_NUMBER() OVER(ORDER BY LAT_N) AS IDX
           , COUNT(*) OVER() + 1 AS CNT
      FROM STATION) AS T
WHERE IDX = CEIL(CNT/2) OR IDX = FLOOR(CNT/2)
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_16_1.png">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (3) 코드 리뷰
오라클에선 중앙값을 구하는 함수를 제공하지만 MySQL은 지원하지 않는다. 그래서 직접 중앙값을 구해야하는데 방법을 모르겠어서 풀이법을 참고해서 문제를 해결했다. 우선 전체 행들 중에서 LAT_N을 기준으로 순서를 나열하기 위해 ROW_NUMBER 함수를 사용했다. 그리고 전체 행의 수를 구하기 위해 COUNT 함수와 OVER 함수를 사용했다. OVER 함수는 GROUP BY 없이 집계함수를 사용할 수 있다. 따로 파티션을 나누지 않고 전체 데이터를 카운트하였다. 중앙값 계산 기준은 전체 행의 개수가 짝수일 때, 중앙에 있는 두개의 값의 평균값이고 홀수일 땐 중앙에 있는 하나의 값이다. 이때 중앙값 계산을 위해 전체 행의 수 + 1 로 CNT 에 담았다. 이를 서브쿼리로 불러왔다. WHERE 문에 IDX가 전체 행의 개수를 2로 나눈값 기준 내림, 올림 했을 때의 값과 같은 데이터만 불러올 수 있도록 조건식을 작성했다. 이렇게 구한 중앙값에 해당하는 행의 평균값을 소수점 4자리 수로 반올림하여 불러왔다.

## 🌞 실패 코드 공유
```sql
SELECT ROUND(AVG(LAT_N), 4)
FROM (SELECT LAT_N
           , ROW_NUMBER() OVER(ORDER BY LAT_N) AS IDX
      FROM STATION) AS T
WHERE IDX = CEIL(COUNT(*)/2) OR IDX = FLOOR(COUNT(*)/2)
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_16_2.png">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

ROW_NUMBER을 사용해서 구해보려고 했으나 총 데이터의 개수(행의 개수)를 구하는 것 때문에 계속 오류가 발생했다. 처음에 다른 풀이법의 도움없이 접근했을 때 아래와 같이 쿼리를 작성했는데 GROUP FUNCTION 을 사용했다는 이유로 에러가 계속 발생했다. 전체 행의 수를 구하는 것에서 계속 문제가 발생했고 이러한 이유로 풀이법을 참고하게 되었다. SET 으로 새로운 변수를 지정하고 COUNT(*) 값을 저장하려고 했으나 집계함수의 사용에 제약이 있어서 사용이 어려웠다. 이번 기회에 GROUP BY 와 GROUP FUNCTION, OVER 함수 간의 관계를 다시 정리해보아야겠다.🔥

<br>

# 2. Reference
- [티스토리 by 유림유림의 블로그, [HackerRank] Weather Observation Station 20 풀이 (Oracle)](https://yurimyurim.tistory.com/14)

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}