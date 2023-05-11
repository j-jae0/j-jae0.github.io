---
title:  "[해커랭크 SQL] ADVANCED JOIN 문제풀이 (1)"
layout: single

categories: "Algorithm_SQL"
tags: ["UNION", "JOIN"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, MEDIUM 1 문제 풀이</small>

***

# 1. Symmetric Pairs
You are given a table, Functions, containing two columns: X and Y.

| Column | Type |
|:-------|:-----|
| X | Integer |
| Y | Integer |

Two pairs (X1, Y1) and (X2, Y2) are said to be symmetric pairs if X1 = Y2 and X2 = Y1.

Write a query to output all such symmetric pairs in ascending order by the value of X. List the rows such that X1 ≤ Y1.

## (1) 코드 작성
```sql
-- x = y
SELECT x, y
FROM functions
GROUP BY x, y
HAVING count(*) > 1

UNION

-- x != y
SELECT f1.x, f1.y
FROM functions AS f1
INNER JOIN functions AS f2 ON f1.x = f2.y AND f2.x = f1.y
WHERE f1.x < f1.y
ORDER BY x
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_10.png" width="70%">
</div>
<center><small>쿼리 실행 결과물</small></center>

<br>

## (2) 코드 리뷰
- 문제는 x, y값의 대칭되는 짝이 있는지를 알아보는 것이다.
- 두 가지 케이스로 나누고 UNION으로 묶어주었다.
  - x, y 값이 같은 경우
  - x, y 값이 다른 경우
- 두 가지 케이스로 나눈 이유는 'x가 y보다 작거나 같다'는 조건과 'x와 y가 같을 수 있다' 때문이다.
- 만약 JOIN으로 x1 = y2, x2 = y1 인 경우를 불러오면 x와 y가 같은 경우는 한 쌍만 있어도 결과에 포함된다.
- 이러한 이유로 x, y가 같은 경우와 다른 경우를 나누어서 불러온 다음 UNION으로 중복을 제거하여 쌍이 존재하는 대칭성을 가지는 x, y값을 불러왔다.


## (3) 회고
처음에 아래와 같이 코드를 작성했을 때 'Wrong Answer' 사인이 떠서 놀랐다. 쿼리가 잘못된 이유를 찾아내기 위해 코드를 한줄씩 없애며 어디서 무엇을 놓친건지 확인해 보았다. ```SELECT * FROM functions AS f1 INNER JOIN functions AS f2 ON f1.x = f2.y AND f2.x = f1.y``` 의 결과를 확인해 보니 x, y 값이 같은 쌍이 하나만 존재해도 JOIN이 가능하기 때문에 결과에 포함되었다. 만약 'Wrong Answer' 사인이 뜨지 않는 상황이라면 쿼리에 문제가 있다는 것을 찾아낼 수 있었을까? 앞으로 코드를 작성할 때, '만족시켜야하는 조건'과 '현재 내가 작성한 코드로부터 생길 수 있는 문제'를 잘 고려해야겠다. 

```sql
-- 실패한 쿼리 공유
SELECT f1.x, f1.y
FROM functions AS f1
INNER JOIN functions AS f2 ON f1.x = f2.y AND f2.x = f1.y
WHERE f1.x <= f1.y
GROUP BY f1.x, f1.y
ORDER BY x
```

[👉 Symmetric Pairs 문제 보러가기](https://www.hackerrank.com/challenges/symmetric-pairs/problem?isFullScreen=true)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}