---
title:  "[해커랭크 SQL] AGGREGATION 문제풀이 (1)"
layout: single

categories: "Algorithm_SQL"
tags: ["ROUND", "SUM", "MIN", "MAX", "TRUNCATE"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, EASY 6 문제 풀이</small>

***

# <span class="half_HL">✔️ 테이블 정보</span>

The ```STATION``` table is described as follows:

|Field|Type|
|:----|:---|
|ID| NUMBER|
|CITY| VARCHAR2(21)|
|STATE| VARCHAR2(2)|
|LAT_N |NUMBER|
|LONG_W| NUMBER|

where ```LAT_N``` is the northern latitude and ```LONG_W``` is the western longitude.

<br>

# <span class="half_HL">1. Weather Observation Station 2</span>
Query the following two values from the **STATION** table:
1. The sum of all values in LAT_N rounded to a scale of 2 decimal places.
2. The sum of all values in LONG_W rounded to a scale of 2 decimal places.

**문제 요약** : ```LAT_N```의 모든 값 합계는 소수점 이하 2자리로 반올림, ```LONG_W```에 있는 모든 값의 합계는 소수점 이하 2자리로 반올림하세요.

## (1) 코드 작성
```sql
SELECT ROUND(SUM(LAT_N), 2), ROUND(SUM(LONG_W), 2)
FROM STATION
```

[👉 Weather Observation Station 2 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-2/problem?isFullScreen=true)

<br>

# <span class="half_HL">2. Weather Observation Station 13</span>
Query the sum of Northern Latitudes (```LAT_N```) from ```STATION``` having values greater than 38.7880 and less than 137.2345. Truncate your answer to 4 decimal places.

**문제 요약** : ```STATION```에서 38.7880보다 크고 137.2345보다 작은 값을 갖는 북위도(```LAT_N```)의 합을 소수점 이하 4 자릿수로 나타내세요.

## (1) 코드 작성
```sql
SELECT TRUNCATE(SUM(LAT_N), 4)
FROM STATION
WHERE LAT_N > 38.7880 AND LAT_N < 137.2345
```

[👉 Weather Observation Station 13 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-13/problem?isFullScreen=true)

<br>

# <span class="half_HL">3. Weather Observation Station 14</span>
Query the greatest value of the Northern Latitudes (```LAT_N```) from ```STATION``` that is less than 137.2345. Truncate your answer to 4 decimal places.

**문제 요약** : ```STATION```에서 137.2345보다 작은 북위도(```LAT_N```)의 최대값을 소수점 4자리로 나타내세요.

## (1) 코드 작성
```sql
SELECT TRUNCATE(MAX(LAT_N), 4)
FROM STATION
WHERE LAT_N < 137.2345
```

[👉 Weather Observation Station 14 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-14/problem?isFullScreen=true)

<br>

# <span class="half_HL">4. Weather Observation Station 15</span>
Query the Western Longitude (```LONG_W```) for the largest Northern Latitude (```LAT_N```) in ```STATION``` that is less than 137.2345. Round your answer to 4 decimal places.

**문제 요약** : ```STATION```에서 137.2345보다 작은 가장 큰 북위(```LAT_N```)에 대해 서경(```LONG_W```)을 소수점 이하 4자리까지 반올림하세요.

## (1) 코드 작성
```sql
SELECT ROUND(LONG_W, 4)
FROM STATION
WHERE LAT_N < 137.2345
ORDER BY LAT_N DESC
LIMIT 1
```

[👉 Weather Observation Station 15 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-15/problem?isFullScreen=true)

<br>

# <span class="half_HL">5. Weather Observation Station 16</span>
Query the smallest Northern Latitude (```LAT_N```) from ```STATION``` that is greater than 38.7780. Round your answer to 4 decimal places.

**문제 요약** : 38.7780보다 큰, 가장 작은 북위도(```LAT_N```)를 쿼리하고 답을 소수점 이하 4자리까지 반올림하세요.

## (1) 코드 작성
```sql
SELECT ROUND(MIN(LAT_N), 4)
FROM STATION
WHERE LAT_N > 38.7780
```

[👉 Weather Observation Station 16 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-16/problem?isFullScreen=true)

<br>

# <span class="half_HL">6. Weather Observation Station 17</span>
Query the Western Longitude (```LONG_W```) where the smallest Northern Latitude (```LAT_N```) in ```STATION``` is greater than 38.7780. Round your answer to 4 decimal places.

**문제 요약** : ```STATION```에서 북위(```LAT_N```)가 38.7780보다 클 때의 가장 작은 서부 경도(```LONG_W```)를 소수점 이하 4자리까지 반올림하세요.

## (1) 코드 작성
```sql
SELECT ROUND(LONG_W, 4)
FROM STATION
WHERE LAT_N > 38.7780
ORDER BY LAT_N 
LIMIT 1
```

[👉 Weather Observation Station 17 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-17/problem?isFullScreen=true)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}