---
title:  "[해커랭크 SQL] ALTERNATIVE QUERIES 문제풀이 (1)"
layout: single

categories: "Algorithm_SQL"
tags: ["SET", "REPEAT", "information_schema.tables"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, EASY 2 문제 풀이</small>

***

# 1. Draw The Triangle 1
P(R) represents a pattern drawn by Julia in R rows. The following pattern represents P(5):

```
* * * * * 
* * * * 
* * * 
* * 
*
```

Write a query to print the pattern P(20).

## (1) 코드 작성
```sql
SET @num = 21;
SELECT repeat('* ', @num:=@num-1)
FROM information_schema.tables
LIMIT 20
```

## (2) 코드 리뷰
- 별 20개를 시작으로 하나씩 줄어드는 결과를 출력해야한다.
  - SET으로 새로운 변수 num을 21로 설정한다.
  - SET으로 변수를 지정할 때, 변수명 앞에 @를 써주고 마지막에 ;를 써줘야한다.
- repeat 함수를 사용해서 '* '가 반복되도록 하고, 반복할 개수를 num에서 1개씩 줄어들게 설정했다.
  - 값을 대입할 땐, := 를 사용해야한다.
- 가상의 테이블을 사용하기 위해 information_schema.tables를 불러왔다.
- 그리고 총 20줄의 별을 불러오기 위해 LIMIT 20 를 작성했다.
  - 하지만 이번 문제에선 LIMIT 20을 작성하지 않아도 num이 0이 되는 순간이 있기 때문에 문제를 통과할 수 있다.
- 처음에 num을 21로 설정한 이유는 @num:=@num-1 식으로 21 - 1 = 20, 첫 줄에서 20개의 별기 위해서이다.


[👉 Draw The Triangle 1 문제 보러가기](https://www.hackerrank.com/challenges/draw-the-triangle-1/problem?isFullScreen=true)

<br>

# 2. Draw The Triangle 2
P(R) represents a pattern drawn by Julia in R rows. The following pattern represents P(5):

```
* 
* * 
* * * 
* * * * 
* * * * *
```

Write a query to print the pattern P(20).

## (1) 코드 작성
```sql
SET @num = 0;
SELECT repeat('* ', @num:=@num+1)
FROM information_schema.tables
LIMIT 20
```

## (2) 코드 리뷰
- 이번 문제는 이전 문제와 거의 동일하다.
- 이전 문제와는 다르게 num 변수를 0으로 설정했고, num를 1개씩 증가시켜서 별의 개수가 늘어날 수 있도록 설정했다.
- 이전과 동일하게 20 줄의 별을 출력하기 위해 LIMIT 20를 작성했다.
  - LIMIT 를 지정하지 않으면 별은 무한대로 증가할 것이다.

[👉 Draw The Triangle 2 문제 보러가기](https://www.hackerrank.com/challenges/draw-the-triangle-2/problem?isFullScreen=true)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}