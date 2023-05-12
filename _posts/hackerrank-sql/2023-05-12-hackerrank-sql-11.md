---
title:  "[해커랭크 SQL] Advanced Select 문제풀이 (2)"
layout: single

categories: "Algorithm_SQL"
tags: ["🌞", "CONCAT", "LEFT", "LOWER"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, MEDIUM 1 문제 풀이</small>

***

# 1. The PADS
Generate the following two result sets:

- Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
- Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format:

```
There are a total of [occupation_count] [occupation]s.
```
where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.

**Note**: There will be at least two entries in the table for each type of occupation.<br>
[👉 The PADS 문제 보러가기](https://www.hackerrank.com/challenges/the-pads/problem?isFullScreen=true)


## (1) 테이블
The **OCCUPATIONS** table is described as follows:

| Column | Type |
|:-------|:-----|
| Name | String |
| Occupation | String |

<small>cf. Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.</small>

## (2) 코드 작성
테이블에 존재하는 사람들의 이름과 직업별로 몇명이 존재하는지 출력해야한다. 모든 이름, 직업별 사람의 수를 출력해야해서 하나의 ```SELECT - FROM``` 문으로 구할 수 없다. 두 케이스를 나누어서 결과를 출력해야 한다.

```sql
SELECT CONCAT(name,  '(', LEFT(occupation, 1), ')')
FROM OCCUPATIONS 
ORDER BY name;

SELECT CONCAT('There are a total of ', COUNT(*), ' ', LOWER(occupation), 's.')
FROM OCCUPATIONS 
GROUP BY occupation
ORDER BY COUNT(*), occupation;
```

## (3) 코드 리뷰
- 다른 형태의 두 정보를 출력해야된다는 점에서 SQL 쿼리문을 두 개를 만들었다.
- 이름과 어떤 직업을 가지고 있는지를 먼저 출력하고 직업별로 몇명이 존재하는지를 문장으로 출력해야 한다.
  - 특히, 두 정보는 각기 다른 정렬 기준을 가진다.
- 문자열을 조합해야되기 때문에 CONCAT 함수를 사용했다.


## 🌞 실패 코드 공유
```sql
-- 실패한 코드 공유
SELECT CONCAT(name,  '(', LEFT(occupation, 1), ')')
FROM (SELECT * 
      FROM OCCUPATIONS 
      ORDER BY name) AS t1

UNION

SELECT CONCAT('There are a total of ', occupation_count, ' ', LOWER(occupation), 's.')
FROM (SELECT occupation, COUNT(*) AS occupation_count 
      FROM OCCUPATIONS 
      GROUP BY occupation
      ORDER BY occupation_count, occupation) AS t2
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_11_1.png">
</div>
<center><small>성공, 실패 쿼리 결과물 비교</small></center>

<br>

- 다른 형태의 두 정보를 출력해야된다는 점에서 서브쿼리로 각각 다른 컬럼을 기준으로 정렬하고 UNION으로 결합하는 방식으로 접근하면 되겠다고 생각했었다.
- 성공과 실패 쿼리 결과물 이미지를 보면 알 수 있듯이 <u>이름의 정렬이 무너진 것을 알 수 있다.</u>
- UNION을 사용하면 기존에 정렬되어있던 서브쿼리의 규칙이 깨지는 것으로 판단된다.(UNION 결과의 정렬은 마지막에 ORDER BY를 적용해야하는데 이번 케이스에서는 적용하기 힘듦)
- ```A UNION B``` 를 했을 때 단순히 A 뒤에 B를 붙인다고 생각했는데 착각이었다. 만약 테이블이 이름을 기준으로 오름차순 정렬되어있었다면 UNION을 사용했을 때 정답 sign이 떴을 것이다.
- 이번 문제를 접하면서 서브쿼리를 생성할 때, 어떤 요소로 인해 정렬이 깨질 수 있다는 것을 알게 되었다.

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}