---
title:  "[해커랭크 SQL] Advanced Select 문제풀이 (3)"
layout: single

categories: "Algorithm_SQL"
tags: ["🌞", "IF", "OVER", "PARTITION BY", "ROW_NUMBER"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, MEDIUM 1 문제 풀이</small>

***

# 1. Occupations
[Pivot](https://en.wikipedia.org/wiki/Pivot_table) the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation. The output column headers should be Doctor, Professor, Singer, and Actor, respectively.

**Note**: Print NULL when there are no more names corresponding to an occupation.<br>
[Occupations 문제 보러가기](https://www.hackerrank.com/challenges/occupations/problem?isFullScreen=true)

## (1) 테이블
The **OCCUPATIONS** table is described as follows:

| Column | Type |
|:-------|:-----|
| Name | String |
| Occupation | String |

<small>cf. Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.</small>


## (2) 문제 이해
직업의 유형을 컬럼으로 설정하고 각 직업을 가진 사람들의 이름을 행으로 불러와야한다. 직업별 최대 이름수보다 적은 컬럼은 빈 셀을 NULL값으로 채워야 한다. 아래 이미지로 쉽게 이해할 수 있다.<br>
<small>cf. 직업별로 이름을 기준으로 오름차순 정렬이 되어야 한다.</small>

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_12_1.png">
</div>
<center><small>INPUT(왼쪽), OUTPUT(오른쪽) 예시</small></center>

<br>

## (3) 코드 작성
```sql
SELECT GROUP_CONCAT(IF(occupation='Doctor', name, NULL)) as 'Doctor',
       GROUP_CONCAT(IF(occupation='Professor', name, NULL)) as 'Professor',
       GROUP_CONCAT(IF(occupation='Singer', name, NULL)) as 'Singer',
       GROUP_CONCAT(IF(occupation='Actor', name, NULL)) as 'Actor'
FROM (SELECT name, 
             occupation, 
             ROW_NUMBER() OVER(PARTITION BY occupation ORDER BY name) AS idx 
      FROM occupations) AS t
GROUP BY idx
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_12_2.png" width="90%">
</div>
<center><small>위 쿼리의 실행 결과물</small></center>

<br>

## (4) 코드 리뷰
- 직업별로 이름을 출력할 때, 행이 아닌 하나의 열에 속하도록 설정해야한다.
  - 피봇 기능 필요(SQL 에서는 따로 피봇을 지원하는 함수가 없음)
- 우선 서브쿼리를 만들어서 직업 및 이름순서별로 행의 순서를 매겨주었다.
- 인덱스(idx) 값을 기준으로 직업별로 값이 존재하면 이름을, 없으면 NULL이 들어갈 수 있도록 IF 문을 사용했다.
  - 참고로 idx값으로 GROUP BY하였기 때문에 직업별로 이름이 순서대로 들어간다.
- GROUP_CONCAT을 사용한 이유는 그룹화했기 때문에 IF문을 단독으로 사용했다가 에러 sign이 떴다. 해결과정은 아래 '실패 코드 공유'에 기록하였다.
- PARTITION BY는 특정 컬럼을 기준으로(그룹화처럼) 분할한다.

### 🔍 이해를 위한 예시
<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_12_4.png" width="85%">
</div>

<br>

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_12_5.png">
</div>

<br>

## 🌞 실패 코드 공유
```sql
SELECT IF(occupation='Doctor', name, NULL) as 'Doctor',
       IF(occupation='Professor', name, NULL) as 'Professor',
       IF(occupation='Singer', name, NULL) as 'Singer',
       IF(occupation='Actor', name, NULL) as 'Actor'
FROM (SELECT name, 
             occupation, 
             ROW_NUMBER() OVER(PARTITION BY occupation ORDER BY name) AS idx 
      FROM occupations) AS t
GROUP BY idx
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_12_3.png" width="90%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

### 🔍 실패 경험 회고
idx를 기준으로 그룹화를 하고 직업별로 이름을 출력하려고 위와같이 쿼리를 작성했을 때 위 이미지와 같은 에러가 발생했다. 그룹화를 했으나 SELECT 문에는 GROUP BY와 관련된 함수를 사용하지 않아서(집계처리가 안된 내용이 있어서) 발생한 문제였다. 그래서 IF ~ 에 해당하는 결과를 그대로 출력할 수 있는(변화없이) 집계함수를 찾다가 ```GROUP_CONCAT```을 사용하여 문제를 해결하였다. <br>
<small>cf. MAX, MIN 등의 집계함수도 사용이 가능했다.</small>

### 🔍 알게된 점
GROUP BY는 GROUP BY에 컬럼만 SELECT절에 그대로 사용할 수 있다. <br>
GROUP BY에 정의하지 않은 컬럼을 SELECT절에서 사용하려면 반드시 집계함수 처리를 해야 한다.

<br>

# 2. Reference
- [WiKiDocs 평생 필요한 데이터 분석 - MySQL과 주식 데이터로 재밌게, 4.09.4 GROUP BY 사용 규칙](https://wikidocs.net/132723)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}