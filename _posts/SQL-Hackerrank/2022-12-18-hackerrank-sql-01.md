---
title:  "[해커랭크 SQL] Basic Select 문제풀이 (1)"
layout: single

categories: "Algorithm_SQL"
tags: ["WHERE"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 EASY 6 문제 풀이</small>

***

# <span class="half_HL">✔️ 테이블 정보</span>

The ```CITY``` table is described as follows:

|Field|Type|
|:----|:---|
|ID| NUMBER|
|NAME| VARCHAR2(17)|
|COUNTRYCODE| VARCHAR2(3)|
|DISTRICT| VARCHAR2(20)|
|POPULATION |NUMBER|

<br>

# <span class="half_HL">1. Select All</span>

Query all columns (attributes) for every row in the ```CITY``` table.

**문제 요약** : ```CITY``` 테이블의 모든 행에 대한 모든 열 출력

```sql
SELECT *
FROM CITY
```

[👉 Select All 문제 보러가기](https://www.hackerrank.com/challenges/select-all-sql/problem?isFullScreen=true)

<br>

# <span class="half_HL">2. Select By ID</span>

Query all columns for a city in ```CITY``` with the ID 1661.

**문제 요약** : ```ID```가 ```1661```인 모든 데이터 출력

```sql
SELECT *
FROM CITY
WHERE ID = 1661
```

[👉 Select By ID 문제 보러가기](https://www.hackerrank.com/challenges/select-by-id/problem?isFullScreen=true)

<br>

# <span class="half_HL">3. Japanese Cities' Attributes</span>
Query all attributes of every Japanese city in the ```CITY``` table. The ```COUNTRYCODE``` for Japan is ```JPN```.

**문제 요약** : ```COUNTRYCODE```가 ```JPN```인 데이터의 모든 열 출력

```sql
SELECT *
FROM CITY
WHERE COUNTRYCODE = 'JPN'
```

[👉 Japanese Cities' Attributes 문제 보러가기](https://www.hackerrank.com/challenges/japanese-cities-attributes/problem?isFullScreen=true)

<br>

# <span class="half_HL">4. Japanese Cities' Names</span>
Query the names of all the Japanese cities in the ```CITY``` table. The ```COUNTRYCODE``` for Japan is ```JPN```.

**문제 요약** : ```COUNTRYCODE```가 ```JPN```인 데이터의 ```NAME``` 컬럼 출력


```sql
SELECT NAME
FROM CITY
WHERE COUNTRYCODE = 'JPN'
```

[👉 Japanese Cities' Names 문제 보러가기](https://www.hackerrank.com/challenges/japanese-cities-name/problem?isFullScreen=true)

<br>

# <span class="half_HL">5. Revising the Select Query I</span>
Query all columns for all American cities in the ```CITY``` table with populations larger than ```100000```. The ```CountryCode``` for America is USA.

**문제 요약**
1. ```POPULATION```이 100000보다 큰 데이터
2. ```COUNTRYCODE```가 ```USA```인 데이터
3. 1, 2번을 만족한 데이터의 모든 열을 출력

```sql
SELECT *
FROM CITY 
WHERE POPULATION > 100000 AND COUNTRYCODE = 'USA'
```

[👉 Revising the Select Query I 문제 보러가기](https://www.hackerrank.com/challenges/revising-the-select-query/problem?isFullScreen=true)

<br>

# <span class="half_HL">6. Revising the Select Query II</span>

Query the ```NAME``` field for all American cities in the ```CITY``` table with populations larger than ```120000```. The CountryCode for America is ```USA```.

**문제 요약**
1. ```POPULATION```이 120000보다 큰 데이터
2. ```COUNTRYCODE```가 ```USA```인 데이터
3. 1, 2번을 만족한 데이터의 ```NAME``` 열만 출력

```sql
SELECT NAME
FROM CITY 
WHERE POPULATION > 120000 AND COUNTRYCODE = 'USA'
```

[👉 Revising the Select Query II 문제 보러가기](https://www.hackerrank.com/challenges/revising-the-select-query-2/problem?isFullScreen=true)

<br>

# <span class="half_HL">➕ 문제풀이 회고</span>
- 이번 문제는 SQL의 기본 문법인 ```SELECT, FROM, WHERE``` 절만 사용하여 해결했다.
- ```WHERE```에 조건을 2개 이상 작성할 때, 두 조건 다 만족해야한다면 ```AND```로 연결해야하고 두 조건 중 하나라도 만족하면 된다면 ```OR```로 연결하면 된다.
- EASY 😎

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}
