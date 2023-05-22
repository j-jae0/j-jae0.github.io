---
title:  "[프로그래머스 Oracle] Lv 1. 상위 n개 레코드"
layout: single

categories: "Algorithm_Oracle"
tags: ["ROWNUM"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - SELECT 문제</small>

***

# 1. 문제 설명
ANIMAL_INS 테이블은 동물 보호소에 들어온 동물의 정보를 담은 테이블입니다. 
<br>ANIMAL_INS 테이블 구조는 다음과 같으며, ANIMAL_ID, ANIMAL_TYPE, DATETIME, INTAKE_CONDITION, NAME, SEX_UPON_INTAKE는 각각 동물의 아이디, 생물 종, 보호 시작일, 보호 시작 시 상태, 이름, 성별 및 중성화 여부를 나타냅니다.

|NAME|	TYPE|	NULLABLE|
|:---|:-----|:----------|
|ANIMAL_ID|	VARCHAR(N)|	FALSE|
|ANIMAL_TYPE|	VARCHAR(N)|	FALSE|
|DATETIME|	DATETIME|	FALSE|
|INTAKE_CONDITION|	VARCHAR(N)|	FALSE|
|NAME|	VARCHAR(N)|	TRUE|
|SEX_UPON_INTAKE|	VARCHAR(N)|	FALSE|

동물 보호소에 가장 먼저 들어온 동물의 이름을 조회하는 SQL 문을 작성해주세요.

본 문제는 Kaggle의 "Austin Animal Center Shelter Intakes and Outcomes"에서 제공하는 데이터를 사용하였으며 ODbL의 적용을 받습니다.
<br>[👀 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/59405?language=oracle)

<br>

# 2. 문제 풀이
## (1) Pseudo-Code
```markdown
1. DATETIME을 기준으로 오름차순정렬한 ANIMAL_INS 테이블을 서브쿼리로 불러온다.
2. 이름만 가져올 수 있도록 SELECT 문에 작성한다.
3. 가장 먼저 들어온 동물의 정보만 불러오기 위해 ROWNUM 으로 첫 번째 행만 불러올 수 있는 조건문을 작성한다.
```

## (2) 코드 작성
```sql
SELECT NAME
FROM (SELECT *
      FROM ANIMAL_INS
      ORDER BY DATETIME)
WHERE ROWNUM = 1
```

## (3) 코드 리뷰 및 회고
- Oracle은 LIMIT 를 지원하지 않는다. 행의 수를 제어할 땐, WHERE 절에서 잘라야한다.
- WHERE 절 적용 후 ORDER BY 문이 적용되지 않기 때문에 서브쿼리를 만들지 않으면 해당 문제를 해결할 수 없다.

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}