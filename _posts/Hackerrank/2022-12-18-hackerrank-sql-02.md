---
title:  "[해커랭크 SQL] Select By ID"
layout: single

categories: "Algorithm_SQL"

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 EASY 문제 풀이</small>

***

# Select By ID
Query all columns for a city in CITY with the ID 1661.

[Select By ID 문제 보러가기](https://www.hackerrank.com/challenges/select-by-id/problem?isFullScreen=true)

## (1) 테이블 정보
The **CITY** table is described as follows:

|Field|Type|
|:----|:---|
|ID| NUMBER|
|NAME| VARCHAR2(17)|
|COUNTRYCODE| VARCHAR2(3)|
|DISTRICT| VARCHAR2(20)|
|POPULATION |NUMBER|

## (2) 문제 이해
테이블에서 ID가 1661인 모든 데이터 출력하는 쿼리를 작성한다.

## (3) 코드 작성
```sql
SELECT *
FROM CITY
WHERE ID = 1661
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_2.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (4) 코드 리뷰
CITY 테이블에서 ID 값이 1661 인 데이터만 불러오기 위해 WHERE 절에서 ID가 1661이다 라는 조건식을 넣었다. 그리고 SELECT 문에 *를 넣어 조건식에 해당하는 행의 모든 열이 출력되도록 쿼리를 작성했다.

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}