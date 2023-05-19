---
title:  "[해커랭크 SQL] Basic Select 문제풀이 (2)"
layout: single

categories: "Algorithm_SQL"
tags: ["LIKE", "REGEXP", "DISTINCT", "COUNT", "LENGTH", "UNION", "NOT LIKE"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 EASY 11 문제 풀이</small>

***

# 📄 테이블 정보
The **STATION** table is described as follows:

|Field|Type|
|:----|:---|
|ID| NUMBER|
|CITY| VARCHAR2(21)|
|STATE| VARCHAR2(2)|
|LAT_N |NUMBER|
|LONG_W| NUMBER|

<small>cf. where LAT_N is the northern latitude and LONG_W is the western longitude.</small>

<br>

# 1. Weather Observation Station 1
Query a list of CITY and STATE from the STATION table.<br>
[📍 Weather Observation Station 1 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-1/problem?isFullScreen=true)

## (1) 문제 이해
테이블에서 모든 데이터의 city, state 정보를 출력하는 쿼리를 작성한다.

## (2) 코드 작성
```sql
SELECT CITY, STATE
FROM STATION
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_7.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

## (3) 코드 리뷰
행을 필터링하는 조건없이 전체 데이터에 대해 컬럼만 CITY, STATE만 불러오기 위해 SELECT 문에 출력하고자 하는 컬럼명만 기입해주었다.

<br>

# 2. Weather Observation Station 3
Query a list of CITY names from STATION for cities that have an even ID number. Print the results in any order, but exclude duplicates from the answer.<br>
[📍 Weather Observation Station 3 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-3/problem?isFullScreen=true)

## (1) 문제 이해
테이블에서 아이디 번호가 짝수인 도시를 출력하는 쿼리를 작성한다. 이때 중복값이 존재하기 때문에 중복 항목을 제외해야한다. 

## (2) 코드 작성
### LIKE 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE ID LIKE '%0'
OR ID LIKE '%2'
OR ID LIKE '%4'
OR ID LIKE '%6'
OR ID LIKE '%8'
```

### REGEXP 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE ID REGEXP '[02468]$'
```

### 수식
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE ID % 2 = 0
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_8.png" width="85%">
</div>
<center><small>위의 세 쿼리의 실행 결과(동일)</small></center>

## (3) 코드 리뷰
이번엔 세 가지 방법으로 문제에 접근해 보았다. ID가 짝수라는 점에서 ID번호의 마지막 숫자가 0, 2, 4, 6, 8 중에 하나일 것이다. 그래서 LIKE 연산자를 사용했을 땐 OR로 조건식을 연결해 주었고 와일드카드 %를 사용하여 앞 번호는 상관없이 맨 뒷자리 번호가 0, 2, 4, 6, 8인 데이터만 불러왔다.

REGEXP 연산자를 사용했을 땐 []안에 있는 요소들로 끝나는($) 데이터만 불러올 수 있도록 하였다.

수식으로는 짝수가 2로 나누었을 때 나머지가 없는 경우이기 때문에 ID를 2로 나누었을 때 나머지가 0이다 라는 조건식을 넣어주었다.

마지막으로 필터링된 데이터의 도시를 출력할 때 중복값이 존재한다는 점에서 중복항목을 제거하기 위해 CITY 앞에 DISTINCT를 작성해주었다. DISTINCT 는 컬럼의 중복항목을 제거해주는 역할을 한다.

<br>

# 3. Weather Observation Station 4
Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.

[📍 Weather Observation Station 4 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-4/problem?isFullScreen=true)

## (1) 문제 이해
CITY의 전체 데이터 개수와 중복 없이 유일한 값을 가지는 데이터 개수의 차이를 계산하는 쿼리를 작성한다.

## (2) 코드 작성
```sql
SELECT COUNT(CITY) - COUNT(DISTINCT CITY)
FROM STATION
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_9.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

## (3) 코드 리뷰
문제는 테이블의 CITY 컬럼의 전체 행의 개수에서 중복이 제거되었을 때의 CITY 행의 개수의 차잇값을 구하는 것이다. 중복을 제거하지 않고 행의 개수를 세기 위해 COUNT 함수를 사용했고, 중복값 제거 후의 행의 개수를 세기 위해 COUNT와 DISTINCT 를 사용했다.

<br>

# 4. Weather Observation Station 5
Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.<br>
[📍 Weather Observation Station 5 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-5/problem?isFullScreen=true)

## (1) 문제 이해
가장 짧은 CITY 이름과 가장 긴 CITY 이름과 각각의 길이를 출력하는 쿼리를 작성한다.

## (2) 코드 작성
### UNION 사용O
```sql
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

### UNION 사용X
```sql
SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY), CITY
LIMIT 1;

SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY) DESC, CITY
LIMIT 1;
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_10.png" width="85%">
</div>
<center><small>위 두 쿼리의 실행 결과(동일)</small></center>

## (3) 코드 리뷰
- 문자열의 길이를 불러오기 위해 LENGTH 함수를 사용했다.
- 조건이 다른 두 항목을 출력해야하기 때문에 두개의 쿼리문을 작성하고 UNION으로 연결해 주었다. 하지만 UNION 없이 두 개의 쿼리문을 작성해도 정답 sign을 받을 수 있다.
- ORDER BY, LIMIT를 이용해서 각 경우에 따라 특정 데이터만 가져왔다.
  - 길이가 짧은 경우 : LENGTH(CITY)를 기준으로 오름차순 후 상위 1개
  - 길이가 긴 경우 : LENGTH(CITY)를 기준으로 내림차순 후 상위 1개

<br>

# 5. Weather Observation Station 6
Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.<br>
[📍 Weather Observation Station 6 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-6/problem?isFullScreen=true)

## (1) 문제 이해
모음(a, e, i, o, u)으로 시작되는 CITY 명을 중복 제거하여 불러오는 쿼리를 작성한다.

## (2) 코드 작성
### LIKE 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE 'a%'
   OR CITY LIKE 'e%'
   OR CITY LIKE 'i%'
   OR CITY LIKE 'o%'
   OR CITY LIKE 'u%'
```

### REGEXP 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[aeiou]'
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_11.png" width="85%">
</div>
<center><small>위 두 쿼리의 실행 결과(동일)</small></center>

## (3) 코드 리뷰
모음으로 시작하는 경우를 불러오기 위해 두 가지 방법을 사용해 보았다. LIKE 연산자를 사용했을 땐 OR로 조건식들을 연결해 주었고 와일드카드로 %를 사용했다. REGEXP 연산자를 사용했을 땐 패턴을 []안에 넣고 패턴으로 시작하는 데이터만 불러와야하기 때문에 ^를 앞에 입력해 주었다. 마지막으로 CITY엔 중복값이 존재하기 때문에 중복 항목을 제거하기 위해 DISTINCT를 추가해주었다.

<br>

# 6. Weather Observation Station 7
Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.<br>
[📍 Weather Observation Station 7 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-7/problem?isFullScreen=true)

## (1) 문제 이해
모음으로 끝나는 CITY 명을 중복 제거하여 불러오는 쿼리를 작성한다.

## (2) 코드 작성
### LIKE 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE '%a'
   OR CITY LIKE '%e'
   OR CITY LIKE '%i'
   OR CITY LIKE '%o'
   OR CITY LIKE '%u'
```

### REGEXP 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '[aeiou]$'
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_12.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

## (3) 코드 리뷰
이번 문제는 이전 문제(Weather Observation Station 6)를 풀었을 때와 풀이가 거의 유사하다. 다른 점이 있다면 조건식에서 LIKE 연산자를 사용했을 땐 와일드카드의 위치가 앞으로 이동했고, REGEXP 연산자를 사용했을 땐 ^를 빼고 []패턴 뒤에 $를 넣어주었다.(패턴으로 끝나는 데이터를 불러오기 위함)

<br>

# 7. Weather Observation Station 8
Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.<br>
[📍 Weather Observation Station 8 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-8/problem?isFullScreen=true)

## (1) 문제 이해
첫 자와 끝 자가 모음인 CITY 명을 중복 제거하여 불러오는 쿼리를 작성한다.

## (2) 코드 작성
### LIKE 연산자
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

### REGEXP 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[aeiou]' AND CITY REGEXP '[aeiou]$'
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_13.png" width="85%">
</div>
<center><small>위 두 쿼리의 실행 결과(동일)</small></center>

## (3) 코드 리뷰
조건은 첫 자와 끝 자가 모음인 도시 명을 중복 제거하여 불러오는 것이다. LIKE와 REGEXP 연산자를 사용할 때, 첫자가 모음인 경우와 끝자가 모음인 경우를 모두 만족할 수 있도록 AND로 연결해 주었다.

<br>

# 8. Weather Observation Station 9
Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.<br>
[📍 Weather Observation Station 9 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-9/problem?isFullScreen=true)

## (1) 문제 이해
모음으로 시작되지 않는 도시 명을 중복 제거하여 출력하는 쿼리를 작성한다.

## (2) 코드 작성
### LIKE 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY NOT LIKE 'a%'
  AND CITY NOT LIKE 'e%'
  AND CITY NOT LIKE 'i%'
  AND CITY NOT LIKE 'o%'
  AND CITY NOT LIKE 'u%'
```

### REGEXP 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[^aeiou]'
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_14.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

## (3) 코드 리뷰
모음으로 시작되지 않는 도시명을 출력하기 위해 LIKE 연산자를 사용했을 땐 조건식들을 AND로 연결해 주었다. OR 이 아닌 AND 를 사용한 이유는 OR로 연결한다면 a로 시작하지 않는 경우라면 출력될 수 있기 때문이다. 조건식은 위에서 부터(첫 번째 줄) 시작하기 때문에 e로 시작하는 경우가 'a로 시작하지 않는다'는 조건에 만족하기 때문에 출력될 수 있다. 그래서 AND로 연결해 주었다.

<br>

# 9. Weather Observation Station 10
Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.<br>
[📍 Weather Observation Station 10 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-10/problem?isFullScreen=true)

## (1) 문제 이해
모음으로 끝나지 않는 도시명을 중복 제거하여 출력하는 쿼리를 작성한다.

## (2) 코드 작성
### LIKE 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY NOT LIKE '%a'
  AND CITY NOT LIKE '%e'
  AND CITY NOT LIKE '%i'
  AND CITY NOT LIKE '%o'
  AND CITY NOT LIKE '%u'
```

### REGEXP 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '[^aeiou]$'
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_15.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

## (3) 코드 리뷰
이번 문제는 이전 문제( Weather Observation Station 9)와는 다르게 LIKE 연산자를 사용했을 땐 와일드 카드의 위치를 바꿔주었고 REGEXP 연산자를 사용했을 땐 [패턴] 앞에 ^를 제거하고 [패턴] 뒤에 $를 추가해 주었다.

<br>

# 10. Weather Observation Station 11
Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.<br>
[📍 Weather Observation Station 11 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-11/problem?isFullScreen=true)

## (1) 문제 이해
모음으로 시작되지 않거나 모음으로 끝나지 않는 도시명을 중복 제거하여 출력하는 쿼리를 작성한다.

## (2) 코드 작성
### LIKE 연산자
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

### REGEXP 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[^aeiou]' OR CITY REGEXP '[^aeiou]$'
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_16.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

## (3) 코드 리뷰
모음으로 시작되지 않거나, 모음으로 끝나지 않는 도시명을 출력하기 위해 두 조건식을 AND가 아닌 OR로 연결해 주었다.

<br>

# 11. Weather Observation Station 12
Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.<br>
[📍 Weather Observation Station 12 문제 보러가기](https://www.hackerrank.com/challenges/weather-observation-station-12/problem?isFullScreen=true)

## (1) 문제 이해
모음으로 시작되지 않고 모음으로 끝나지 않는 도시명을 중복 제거하여 출력하는 쿼리를 작성한다.

## (2) 코드 작성
### LIKE 연산자
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

### REGEXP 연산자
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[^aeiou]' AND CITY REGEXP '[^aeiou]$'
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_17.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

## (3) 코드 리뷰
모음으로 시작되지 않고 모음으로 끝나지 않는 도시명을 출력하기 위해 두 조건식을 모두 만족하기 위해 OR이 아닌 AND로 연결해 주었다.

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}