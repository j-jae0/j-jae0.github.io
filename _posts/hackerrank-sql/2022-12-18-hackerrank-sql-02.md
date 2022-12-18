---
title:  "[해커랭크 SQL] BASIC SELECT 문제풀이 (2)"
layout: single

categories: "Algorithm_SQL"
tags: ["WHERE", "LIKE", "REGEXP", "UNION", "ORDER BY", "LIMIT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) 난이도 EASY, 11 문제 풀이</small>

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

# <span class="half_HL">1. Weather Observation Station 1</span>
Query a list of ```CITY``` and ```STATE``` from the ```STATION``` table.
<br>**요약** : ```STATION``` 테이블의 ```CITY```, ```STATE``` 컬럼에 해당하는 데이터 출력

## (1) 코드 작성
```sql
SELECT CITY, STATE
FROM STATION
```

[👉 Weather Observation Station 1 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-1/problem?isFullScreen=true)

<br>

# <span class="half_HL">2. Weather Observation Station 3</span>

Query a list of ```CITY``` names from ```STATION``` for cities that have an even ```ID``` number. Print the results in any order, but exclude duplicates from the answer.
<br>**요약** : ```ID``` 값이 짝수인 ```CITY``` 이름 데이터를 중복 제거하여 출력

## (1) 코드 작성 - LIKE
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE ID LIKE '%0'
OR ID LIKE '%2'
OR ID LIKE '%4'
OR ID LIKE '%6'
OR ID LIKE '%8'
```

## (2) 코드 작성 - REGEXP
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE ID REGEXP '[02468]$'
```

## (3) 코드 작성 - 수식
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE ID % 2 = 0
```

[👉 Weather Observation Station 3 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-3/problem?isFullScreen=true)

<br>

# <span class="half_HL">3. Weather Observation Station 4</span>

Find the difference between the total number of ```CITY``` entries in the table and the number of distinct ```CITY```    entries in the table.

> For example, if there are three records in the table with CITY values 'New York', 'New York', 'Bengalaru', there are 2 different city names: 'New York' and 'Bengalaru'. The query returns , because <br>
**total number of records - number of unique city names = 3 - 2 = 1.**

<br>**요약** : ```CITY```의 전체 데이터 개수와 중복 없이 유일한 값을 가지는 데이터 개수의 차이

## (1) 코드 작성
```sql
SELECT COUNT(CITY) - COUNT(DISTINCT CITY)
FROM STATION
```

[👉 Weather Observation Station 4 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-4/problem?isFullScreen=true)

<br>

# <span class="half_HL">4. Weather Observation Station 5</span>
Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.
<br>**요약** : 가장 짧은 ```CITY``` 이름과 가장 긴 ```CITY``` 이름과 각각의 길이를 출력

## (1) 코드 작성
```python
(SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY), CITY
LIMIT 1)

UNION

(SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY) DESC, CITY
LIMIT 1)
```

[👉 Weather Observation Station 5 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-5/problem?isFullScreen=true)

<br>

# <span class="half_HL">5. Weather Observation Station 6</span>
Query the list of ```CITY``` names starting with vowels (i.e., ```a```, ```e```, ```i```, ```o```, or ```u```) from ```STATION```. Your result cannot contain duplicates.
<br>**요약** : 모음으로 시작되는 ```CITY``` 명을 중복 제거하여 출력

## (1) 코드 작성 - LIKE
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE 'a%'
   OR CITY LIKE 'e%'
   OR CITY LIKE 'i%'
   OR CITY LIKE 'o%'
   OR CITY LIKE 'u%'
```

## (2) 코드 작성 - REGEXP
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[aeiou]'
```

[👉 Weather Observation Station 6 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-6/problem?isFullScreen=true)

<br>

# <span class="half_HL">6. Weather Observation Station 7</span>
Query the list of ```CITY``` names ending with vowels (```a```, ```e```, ```i```, ```o```, ```u```) from ```STATION```. Your result cannot contain duplicates.
<br>**요약** : 모음으로 끝나는 ```CITY``` 명을 중복 제거하여 출력

## (1) 코드 작성 - LIKE
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE '%a'
   OR CITY LIKE '%e'
   OR CITY LIKE '%i'
   OR CITY LIKE '%o'
   OR CITY LIKE '%u'
```

## (2) 코드 작성 - REGEXP
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '[aeiou]$'
```

[👉 Weather Observation Station 7 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-7/problem?isFullScreen=true)

<br>

# <span class="half_HL">7. Weather Observation Station 8</span>
Query the list of ```CITY``` names from ```STATION``` which have vowels (i.e., ```a```, ```e```, ```i```, ```o```, and ```u```) as both their first and last characters. Your result cannot contain duplicates.
<br>**요약** : 첫 자와 끝 자가 모음인 ```CITY``` 명을 중복 제거하여 출력

## (1) 코드 작성 - LIKE
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE (CITY LIKE 'a%'
    OR CITY LIKE 'e%'
    OR CITY LIKE 'i%'
    OR CITY LIKE 'o%'
    OR CITY LIKE 'u%')
    AND (CITY LIKE '%a'
    OR CITY LIKE '%e'
    OR CITY LIKE '%i'
    OR CITY LIKE '%o'
    OR CITY LIKE '%u')
```

## (2) 코드 작성 - REGEXP
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[aeiou]' AND CITY REGEXP '[aeiou]$'
```

[👉 Weather Observation Station 8 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-8/problem?isFullScreen=true)

<br>

# <span class="half_HL">8. Weather Observation Station 9</span>
Query the list of ```CITY``` names from ```STATION``` that do not start with vowels. Your result cannot contain duplicates.
<br>**요약** : 모음으로 시작되지 않는 ```CITY``` 명을 중복 제거하여 출력

## (1) 코드 작성 - LIKE
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY NOT LIKE 'a%'
  AND CITY NOT LIKE 'e%'
  AND CITY NOT LIKE 'i%'
  AND CITY NOT LIKE 'o%'
  AND CITY NOT LIKE 'u%'
```

## (2) 코드 작성 - REGEXP
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[^aeiou]'
```

[👉 Weather Observation Station 9 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-9/problem?isFullScreen=true)

<br>

# <span class="half_HL">9. Weather Observation Station 10</span>

Query the list of ```CITY``` names from ```STATION``` that do not end with vowels. Your result cannot contain duplicates.
<br>**요약** : 모음으로 끝나지 않는 ```CITY``` 명을 중복 제거하여 출력

## (1) 코드 작성 - LIKE
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY NOT LIKE '%a'
  AND CITY NOT LIKE '%e'
  AND CITY NOT LIKE '%i'
  AND CITY NOT LIKE '%o'
  AND CITY NOT LIKE '%u'
```

## (2) 코드 작성 - REGEXP
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '[^aeiou]$'
```

[👉 Weather Observation Station 10 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-10/problem?isFullScreen=true)

<br>

# <span class="half_HL">10. Weather Observation Station 11</span>
Query the list of ```CITY``` names from ```STATION``` that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.
<br>**요약** : 모음으로 시작되지 않거나 모음으로 끝나지 않는 ```CITY``` 명을 중복 제거하여 출력

## (1) 코드 작성 - LIKE
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE (CITY NOT LIKE 'a%'
   AND CITY NOT LIKE 'e%'
   AND CITY NOT LIKE 'i%'
   AND CITY NOT LIKE 'o%'
   AND CITY NOT LIKE 'u%')
   OR (CITY NOT LIKE '%a'
   AND CITY NOT LIKE '%e'
   AND CITY NOT LIKE '%i'
   AND CITY NOT LIKE '%o'
   AND CITY NOT LIKE '%u')
```

## (2) 코드 작성 - REGEXP
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[^aeiou]' OR CITY REGEXP '[^aeiou]$'
```

[👉 Weather Observation Station 11 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-11/problem?isFullScreen=true)

<br>

# <span class="half_HL">11. Weather Observation Station 12</span>
Query the list of ```CITY``` names from ```STATION``` that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.
<br>**요약** : 모음으로 시작되지 않고 모음으로 끝나지 않는 CITY 명을 중복 제거하여 출력

## (1) 코드 작성 - LIKE
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY NOT LIKE 'a%'
  AND CITY NOT LIKE 'e%'
  AND CITY NOT LIKE 'i%'
  AND CITY NOT LIKE 'o%'
  AND CITY NOT LIKE 'u%'
  AND CITY NOT LIKE '%a'
  AND CITY NOT LIKE '%e'
  AND CITY NOT LIKE '%i'
  AND CITY NOT LIKE '%o'
  AND CITY NOT LIKE '%u'
```

## (2) 코드 작성 - REGEXP
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[^aeiou]' AND CITY REGEXP '[^aeiou]$'
```

[👉 Weather Observation Station 12 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-12/problem?isFullScreen=true)

<br>

# <span class="half_HL">➕ 문제풀이 회고</span>
- **WHERE 조건문**을 작성할 때, 특정 문자열에 대해 검색할 땐 **LIKE** 또는 **REGEXP** 연산자를 사용하면 된다.
- **REGEXP** 사용 시, []안에 들어간 문자패턴을 포함하면 조건식이 만족된다.
  - ```[^패턴]``` : 패턴을 포함하지 않는 경우
  - ```^[패턴]``` : 패턴으로 시작되는 경우
  - ```[패턴]$``` : 패턴으로 끝나는 경우
- **LIKE** 사용 시, 2개 이상의 조건을 사용한다면 AND, OR 을 구분해서 사용해야한다.
  - ```AND``` : 여러 조건들이 모두 만족되어야만 출력
  - ```OR``` : 여러 조건들 중 하나만 만족해도 출력
- **문제 : Weather Observation Station 5**
  - **UNION**을 사용해서 두 경우로 **CITY명이 짧은 경우** / **CITY명이 긴 경우**를 합쳤다.
  - **ORDER BY**, **LIMIT**를 이용해서 특정 데이터만 가져왔다.

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}
