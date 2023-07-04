---
title:  "[해커랭크 SQL] Advanced Select 문제풀이 (1)"
layout: single

categories: "Algorithm_SQL"
tags: ["CASE"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 EASY 1 문제 풀이</small>

***

# ✔️ 테이블 정보

The **TRIANGLES** table is described as follows:

| Column | Type |
|:-------|:-----|
| A | Integer |
| B | Integer |
| C | Integer |

<br>

# 1. Type of Triangle
Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:

- Equilateral: It's a triangle with 3 sides of equal length.
- Isosceles: It's a triangle with 2 sides of equal length.
- Scalene: It's a triangle with 3 sides of differing lengths.
- Not A Triangle: The given values of A, B, and C don't form a triangle.

**문제 요약** : 주어지는 세 변의 정보를 가지고 어떤 삼각형인지 분류하세요.

## (1) 코드 작성
```sql
SELECT CASE
         WHEN C >= (A+B) OR A >= (B+C) OR B >= (A+C) THEN 'Not A Triangle'
         WHEN A = B AND A = C THEN 'Equilateral'
         WHEN A != B AND A != C AND B != C THEN 'Scalene' ELSE 'Isosceles'
       END AS Results
FROM TRIANGLES
```

## (2) 코드 리뷰
- 삼각형의 종류는 총 3가지이고 삼각형이 되지 못하는 경우를 포함해서 총 4가지 결과를 세 변의 길이 정보를 이용해서 분류해야한다.
  - 정삼각형 : 세 변의 길이가 모두 동일
  - 이등변삼각형 : 두 변의 길이가 동일
  - 부등변삼각형 : 세 변의 길이가 모두 다름
  - 삼각형X : 삼각형이 되지 못함
- 총 4가지에 대한 결과를 나타내야하기 때문에 CASE 문을 사용했다.
- 삼각형이 되지 못하는 조건은, 두 변의 합이 나머지 변의 길이보다 같거나 작을 경우이다. OR로 세 경우 중 하나만 만족하더라도 'Not A Triangle'이 출력되도록 조건식을 작성했다.
- 정삼각형이 되는 조건은 A = B, A = C 로 작성하면 나머지 B = C 가 해결되는 것이므로 다음과 같이 작성했다.
- 부등변삼각형이 되는 조건은 세 변의 길이가 서로 같지 않다는 식을 AND로 연결해 세 식이 다 만족하게 설정했다.
- 그 외의 결과는 이등변삼각형으로 출력되게끔 ELSE 뒤에 'Isosceles'를 작성했다.
- 삼각형이 되지 못하는 조건식을 첫 번째에 작성한 이유는 삼각형이 되지 못하는 경우와 될 수 있는 경우를 첫번째에 판단하기 위해서이다.


[👉 Type of Triangle 문제 보러가기](https://www.hackerrank.com/challenges/what-type-of-triangle/problem?isFullScreen=true)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}