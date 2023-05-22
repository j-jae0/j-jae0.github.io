---
title:  "[프로그래머스 Oracle] Lv 1. 동물의 아이디와 이름"
layout: single

categories: "Algorithm_Oracle"

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

동물 보호소에 들어온 모든 동물의 아이디와 이름을 ANIMAL_ID순으로 조회하는 SQL문을 작성해주세요.
<br>SQL을 실행하면 다음과 같이 출력되어야 합니다.

|ANIMAL_ID|	NAME|
|:--------|:----|
|A349996|	Sugar|
|A350276|	Jewel|
|A350375|	Meo|
|A352555|	Harley|
|A352713|	Gia|
|A352872|	Peanutbutter|
|A353259|	Bj|

((이하 생략))

본 문제는 Kaggle의 "Austin Animal Center Shelter Intakes and Outcomes"에서 제공하는 데이터를 사용하였으며 ODbL의 적용을 받습니다.
<br>[👀 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/59403?language=oracle)

<br>

# 2. 문제 풀이
## (1) Pseudo-Code
```markdown
1. ANIMAL_INS 테이블을 가져온다.
2. 아이디와 이름값만 반환하여 가져올 수 있도록 SELECT 문에 작성한다. 
4. ANIMAL_ID를 기준으로 오름차순 정렬한다.
```

## (2) 코드 작성
```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

## (3) 코드 리뷰 및 회고
- EASY 😎

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}