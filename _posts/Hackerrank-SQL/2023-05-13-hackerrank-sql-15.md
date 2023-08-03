---
title:  "[해커랭크 SQL] Aggregation 문제풀이 (4)"
layout: single

categories: "Algorithm_SQL"
tags: ["ROUND", "MIN", "MAX", "POW", "SQRT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 MEDIUM 2 문제 풀이</small>

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

# 1. Weather Observation Station 18

Consider P1(a, b) and P2(c, d) to be two points on a 2D plane.

- a happens to equal the minimum value in Northern Latitude (LAT_N in STATION).
- b happens to equal the minimum value in Western Longitude (LONG_W in STATION).
- c happens to equal the maximum value in Northern Latitude (LAT_N in STATION).
- d happens to equal the maximum value in Western Longitude (LONG_W in STATION).

Query the Manhattan Distance between points P1 and P2 and round it to a scale of  decimal places.

## (1) 문제 이해
STAION 테이블의 LAT_N과 LONG_W가 좌표의 x, y 값이 되어 최댓값과 최솟값 사이의 맨해튼 거리를 구한다. 거리를 구하는 공식은 아래 수식과 같다.

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_15_md.png" width="70%">
</div>
<center><small>맨해튼 거리 공식(제작: PowerPoint)</small></center>

<br>

## (2) 코드 작성
```sql
SELECT ROUND((MAX(LAT_N) - MIN(LAT_N)) + (MAX(LONG_W) - MIN(LONG_W)), 4)
FROM STATION
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_15_1.png">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (3) 코드 리뷰
- 맨해튼 거리는 x끼리의 거리 절댓값과 y끼리의 거리 절댓값을 더한 결과이다.
- 수식을 보면 절댓값처리가 되어있는데 쿼리를 작성할 때 따로 절댓값 처리를 하지 않으려고 최댓값에서 최솟값을 뺐다.
- 각 x, y값의 최댓값 최솟값은 MAX, MIN 함수를 사용했다.
- 결과는 반올림하여 소수점 4자리수로 표현해야해서 ROUND 함수를 사용했다.
- EASY 😎

<br>

# 2. Weather Observation Station 19

Consider P1(a, c) and  P2(b, d) to be two points on a 2D plane where  are the respective minimum and maximum values of Northern Latitude (LAT_N) and  are the respective minimum and maximum values of Western Longitude (LONG_W) in STATION.

Query the Euclidean Distance between points P1 and P2 and format your answer to display 4 decimal digits.

## (1) 문제 이해
STAION 테이블의 LAT_N과 LONG_W가 좌표의 x, y 값이 되어 최댓값과 최솟값 사이의 유클리드 거리를 구한다. 거리를 구하는 공식은 아래 수식과 같다.

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_15_ud.png">
</div>
<center><small>유클리드 거리 공식(제작: PowerPoint)</small></center>

<br>

## (2) 코드 작성
```sql
SELECT ROUND(SQRT(POW(MAX(LAT_N)-MIN(LAT_N), 2) + POW(MAX(LONG_W)-MIN(LONG_W), 2)), 4)
FROM STATION
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_15_2.png">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (3) 코드 리뷰
- 유클리드 거리를 구하는 공식(~피타고라스)에 맞게 쿼리를 작성했다.
- x의 거리, y의 거리값을 제곱하기 위해 POW 함수를 사용했다.
- 각 좌표의 거리의 제곱값을 루트 취하기 위해(제곱근) SQRT 함수를 사용했다.
- 최종적으로 유클리드 거리를 출력할 때, 반올림하여 소수점 4자리수로 가져오기 위해 ROUND 함수를 사용했다.
- EASY 😎

<br>

# 3. Reference 
- [Weather Observation Station 18 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-18/problem?isFullScreen=true)
- [Weather Observation Station 19 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-19/problem?isFullScreen=true)
- [Manhattan distance 참고자료](https://xlinux.nist.gov/dads/HTML/manhattanDistance.html)
- [Euclidean distance 참고자료](https://en.wikipedia.org/wiki/Euclidean_distance)

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}