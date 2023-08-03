---
title:  "[프로그래머스 Oracle] Lv 1. 이름이 있는 동물의 아이디"
layout: single

categories: "Algorithm_SQL"
tags: ["IS NOT NULL"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - IS NULL 문제</small>

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

동물 보호소에 들어온 동물 중, 이름이 있는 동물의 ID를 조회하는 SQL 문을 작성해주세요. 단, ID는 오름차순 정렬되어야 합니다.

본 문제는 Kaggle의 "Austin Animal Center Shelter Intakes and Outcomes"에서 제공하는 데이터를 사용하였으며 ODbL의 적용을 받습니다.
<br>[👀 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/59407)

<br>

# 2. 문제 풀이
## (1) Pseudo-Code
```markdown
1. ANIMAL_INS 테이블을 가져온다.
2. 아이디만 가져올 수 있도록 SELECT 문에 작성한다.
3. 이름이 있는 동물 정보를 불러오기 위해 WHERE 절에 '이름이 존재한다'는 조건식을 넣는다.
4. 아이디를 기준으로 오름차순 정렬한다.
```

## (2) 코드 작성
```sql
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
ORDER BY ANIMAL_ID
```

## (3) 코드 리뷰 및 회고
- EASY 😎

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}