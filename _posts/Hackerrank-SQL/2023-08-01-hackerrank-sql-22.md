---
title:  "[해커랭크 SQL] Basic Join 문제풀이 (5)"
excerpt: "해커랭크(HackerRank) MySQL, 난이도 MEDIUM 1 문제 풀이"
layout: single

categories: "Algorithm_SQL"
tags: ["JOIN", "IN"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

***

# Ollivander's Inventory
Harry Potter and his friends are at Ollivander's with Ron, finally replacing Charlie's old broken wand.<br>
Hermione decides the best way to choose is by determining the minimum number of gold galleons needed to buy each non-evil wand of high power and age. Write a query to print the id, age, coins_needed, and power of the wands that Ron's interested in, sorted in order of descending power. If more than one wand has same power, sort the result in order of descending age.

[🧙‍♀️🧙🧙‍♂️ Ollivander's Inventory 문제 보러가기](https://www.hackerrank.com/challenges/harry-potter-and-wands/problem?isFullScreen=true)

## (1) 테이블 정보
```Wands```: The id is the id of the wand, code is the code of the wand, coins_needed is the total number of gold galleons needed to buy the wand, and power denotes the quality of the wand (the higher the power, the better the wand is).

<div style="text-align : center;">
<img src="https://s3.amazonaws.com/hr-challenge-images/19502/1458538092-b2a8163a74-ScreenShot2016-03-08at12.13.39AM.png" width="40%">
</div>

```:Wands_Property```:: The code is the code of the wand, age is the age of the wand, and is_evil denotes whether the wand is good for the dark arts. If the value of is_evil is 0, it means that the wand is not evil. The mapping between code and age is one-one, meaning that if there are two pairs, (code1, age1) and (code2, age2), then code1 ≠	code2 and age1 ≠ age2.

<div style="text-align : center;">
<img src="https://s3.amazonaws.com/hr-challenge-images/19502/1458538221-18c4092b7d-ScreenShot2016-03-08at12.13.53AM.png" width="40%">
</div>

## (2) 문제 이해
헤르미온느는 지팡이를 교체하려고 한다. 구매하려는 지팡이는 not evil하고 power와 age가 큰 것이다. 만약 power와 age가 동일하다면 저렴한 지팡이 하나를 대표로 출력한다.
1. 지팡이는 ```not evil``` 할 것
2. 지팡이의 ```power```와 ```age```가 동일하다면 최저가 지팡이 하나를 출력할 것
3. 지팡이 목록은 ```power```을 기준으로 내림차순, ```power```가 동일하다면 ```age```를 기준으로 내림차순 할 것

## (3) 코드 작성
```sql
SELECT W.id, WP.age, W.coins_needed, W.power
FROM Wands AS W
INNER JOIN Wands_Property AS WP ON W.code = WP.code
WHERE WP.is_evil = 0 
AND (W.code, W.power, W.coins_needed) IN (SELECT code
                                               , power
                                               , MIN(coins_needed) AS min_coins
                                          FROM Wands
                                          GROUP BY code, power)
ORDER BY W.power DESC, WP.age DESC
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_18.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (4) 코드 리뷰
지팡이의 id, code, coins_needed, power 정보가 담긴 Wands 테이블에 Wands_Property 테이블을 code를 기준으로 INNER JOIN 하였다(age 정보를 가져오기 위함). 그리고 not evil 한 지팡이만 목록에 담기 위해 WHERE 문으로 조건을 넣어주었다(문제 이해 중 1번). 그리고 2번 조건을 만족시키기 위해 서브쿼리를 만들어 age, power 이 동일할 땐 최저가 지팡이만 불러올 수 있도록 작성했다(age 대신 code로 일치 여부를 작성해도 됨, 같은 코드는 같은 age를 가지기 때문).

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}