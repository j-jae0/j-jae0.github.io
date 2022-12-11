---
title:  ""
layout: single

categories: "Algorithm_SQL"
tags: [""]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"

published: false
---

# 📝 문제
- 문제는 [HackerRank](https://www.hackerrank.com/dashboard)에 등록되어 있음
- 모든 문제는 아래에 첨부한 ```CITY``` 테이블 사용
- 데이터베이스로는 ```MySQL```을 사용

<br><small>**테이블 명 : CITY**</small>

| Field | Type |
|:----------|:----------|
| ID | NUMBER |
| NAME | VARCHAR2(17) |
| COUNTRYCODE | VARCHAR2(3) |
| DISTRICT | VARCHAR2(20) |
| POPULATION | NUMBER |

------
### 📍 1번 문제
Query all columns (attributes) for every row in the **CITY** table. <br>
: CITY 테이블의 모든 행에 대한 모든 열 출력


```sql
SELECT *
FROM city
```

[문제 1. Select All](https://www.hackerrank.com/challenges/select-all-sql/problem?isFullScreen=true)

------

### 📍 2번 문제
> Query all columns for a city in **CITY** with the ID ```1661```.
```markdown
: ID가 1661인 데이터의 모든 열을 출력
```

```sql
SELECT *
FROM city
WHERE id = 1661
```

&nbsp;&nbsp;&nbsp;<small>[문제 2. Select By ID](https://www.hackerrank.com/challenges/select-by-id/problem?isFullScreen=true)</small>

-----

### 📍 3번 문제
> Query all attributes of every Japanese city in the **CITY** table. The COUNTRYCODE for Japan is ```JPN```.
```markdown
: countrycode가 JPN인 데이터의 모든 열을 출력
```

```sql
SELECT *
FROM city
WHERE countrycode = 'JPN'
```

&nbsp;&nbsp;&nbsp;<small>[문제 3. Japanese Cities’ Attributes](https://www.hackerrank.com/challenges/japanese-cities-attributes/problem?isFullScreen=true)</small>

------
### 📍 4번 문제
> Query the names of all the Japanese cities in the **CITY** table. The COUNTRYCODE for Japan is ```JPN```.
```markdown
: countrycode가 JPN인 데이터의 name 열 출력
```

```sql
SELECT name
FROM city
WHERE countrycode = 'JPN'
```

&nbsp;&nbsp;&nbsp;<small>[문제 4. Japanese Cities’ Names](https://www.hackerrank.com/challenges/japanese-cities-name/problem?isFullScreen=true)</small>

-----
### 📍 5번 문제

> Query all columns for all American cities in the **CITY** table with populations larger than 100000. The CountryCode for America is ```USA```.
```markdown
🔥 문제 요약
1. popluation이 100000보다 큰 데이터
2. countrycode가 USA인 데이터 
3. 1, 2번을 만족한 데이터의 모든 열을 출력
  ```

```sql
SELECT *
FROM CITY 
WHERE population > 100000 AND countrycode = 'USA' 
```
 
&nbsp;&nbsp;&nbsp;<small>[문제 5. Revising the select query1](https://www.hackerrank.com/challenges/revising-the-select-query/problem?isFullScreen=true)</small>

------

### 📍 6번 문제
> Query the NAME field for all American cities in the **CITY** table with populations larger than 120000. The CountryCode for America is ```USA```.
```markdown
🔥 문제 요약
1. population이 120000보다 큰 데이터 
2. countrycode가 USA인 데이터 
3. 1, 2번을 만족한 데이터의 NAME 열만 출력 
```

```sql
SELECT name
FROM city
WHERE population > 120000 AND countrycode = 'USA'
```



&nbsp;&nbsp;&nbsp;<small>[문제 6. Revising the select query2](https://www.hackerrank.com/challenges/revising-the-select-query-2/problem?isFullScreen=true)</small>

------
