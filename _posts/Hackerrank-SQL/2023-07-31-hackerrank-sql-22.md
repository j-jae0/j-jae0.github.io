---
title:  "[해커랭크 SQL] Basic Join 문제풀이 (5)"
excerpt: "해커랭크(HackerRank) MySQL, 난이도 MEDIUM 1 문제 풀이"
layout: single

categories: "Algorithm_SQL"
tags: [""]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
published: false
---

***

# Ollivander's Inventory
Harry Potter and his friends are at Ollivander's with Ron, finally replacing Charlie's old broken wand.<br>
Hermione decides the best way to choose is by determining the minimum number of gold galleons needed to buy each non-evil wand of high power and age. Write a query to print the id, age, coins_needed, and power of the wands that Ron's interested in, sorted in order of descending power. If more than one wand has same power, sort the result in order of descending age.

[📍  문제 보러가기]()

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


## (3) 코드 작성
```sql

```

<div style="text-align : center;">
<img src="/assets/images/algorithm/" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (4) 코드 리뷰


👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}