---
title:  "[프로그래머스 SQL] Lv 4. 그룹별 조건에 맞는 식당 목록 출력하기"
layout: single

categories: "Algorithm_SQL"
tags: ["COUNT", "JOIN", "DATE_FORMAT", "GROUP BY", "ORDER BY", "LIMIT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - JOIN 문제</small>

***

# <span class="half_HL">✔️ 문제 설명</span>
다음은 식당의 정보를 담은 ```REST_INFO```테이블과 식당의 리뷰 정보를 담은 ```REST_REVIEW``` 테이블입니다. ```MEMBER_PROFILE``` 테이블은 다음과 같으며 ```MEMBER_ID```, ```MEMBER_NAME```, ```TLNO```, ```GENDER```, ```DATE_OF_BIRTH```는 회원 ID, 회원 이름, 회원 연락처, 성별, 생년월일을 의미합니다.

|Column name|	Type|	Nullable|
|:---------|:------|:-----------|
|MEMBER_ID|	VARCHAR(100)|	FALSE|
|MEMBER_NAME|	VARCHAR(50)|	FALSE|
|TLNO|	VARCHAR(50)|	TRUE|
|GENDER	|VARCHAR(1)|	TRUE|
|DATE_OF_BIRTH|	DATE|	TRUE|

```REST_REVIEW``` 테이블은 다음과 같으며 ```REVIEW_ID```, ```REST_ID```, ```MEMBER_ID```, ```REVIEW_SCORE```, ```REVIEW_TEXT```, ```REVIEW_DATE```는 각각 리뷰 ID, 식당 ID, 회원 ID, 점수, 리뷰 텍스트, 리뷰 작성일을 의미합니다.

|Column name|	Type	|Nullable|
|:-----|:-----|:-----|
|REVIEW_ID|	VARCHAR(10)	|FALSE|
|REST_ID|	VARCHAR(10)	|TRUE|
|MEMBER_ID|	VARCHAR(100)|	TRUE|
|REVIEW_SCORE|	NUMBER	|TRUE|
|REVIEW_TEXT|	VARCHAR(1000)|	TRUE|
|REVIEW_DATE|	DATE	|TRUE|

## 문제
```MEMBER_PROFILE```와 ```REST_REVIEW``` 테이블에서 리뷰를 가장 많이 작성한 회원의 리뷰들을 조회하는 SQL문을 작성해주세요. 회원 이름, 리뷰 텍스트, 리뷰 작성일이 출력되도록 작성해주시고, 결과는 리뷰 작성일을 기준으로 오름차순, 리뷰 작성일이 같다면 리뷰 텍스트를 기준으로 오름차순 정렬해주세요. 
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/131124)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) Pseudo-Code
1. 리뷰 정보가 포함된 ```REST_REVIEW``` 테이블을 고객 아이디로 그룹화하고 리뷰 횟수를 집계하는 ```REST_REVIEW```와 ```JOIN```한다.
  - 고객 아이디를 기준으로 고객별로 리뷰를 몇번남겼는지 알기 위함
  - 리뷰 횟수를 기준으로 정렬하고 리뷰 1위 정보만 불러와 기존의 ```REST_REVIEW``` 테이블과 합치기
2. 회원 정보가 포함된 ```MEMBER_PROFILE``` 테이블을 고객 아이디를 기준으로 ```JOIN``` 한다.
3. 고객 이름과 리뷰 텍스트, 리뷰 작성일(연월일 형태) 정보를 불러온다.
4. 출력할 데이터는 리뷰 작성일과 리뷰 텍스트를 기준으로 오름차순 정렬한다.


## (2) 코드 작성
```sql
SELECT T2.MEMBER_NAME, RR.REVIEW_TEXT, DATE_FORMAT(RR.REVIEW_DATE, '%Y-%m-%d') AS REVIEW_DATE
FROM REST_REVIEW AS RR
JOIN (
    SELECT MEMBER_ID, COUNT(*) AS ID_COUNT
    FROM REST_REVIEW
    GROUP BY MEMBER_ID
    ORDER BY ID_COUNT DESC
    LIMIT 1
     ) AS T1 ON RR.MEMBER_ID = T1.MEMBER_ID
JOIN (
    SELECT MEMBER_ID, MEMBER_NAME
    FROM MEMBER_PROFILE
     ) AS T2 ON RR.MEMBER_ID = T2.MEMBER_ID
ORDER BY REVIEW_DATE, REVIEW_TEXT
```

## (3) 코드 리뷰 및 회고
- 리뷰를 가장 많이 남긴 회원 정보를 불러오기 위해 ```JOIN-SELECT-FROM-GROUP BY-ORDER BY-LIMIT``` 로 ```REST_REVIEW```에 ```REST_REVIEW```를 JOIN 했다.
  - 이렇게 리뷰를 가장 많이 남긴 고객의 리뷰 정보들을 출력할 수 있다.
- 고객 정보(이름)을 출력하기 위해 ```MEMBER_PROFILE``` 테이블을 고객 아이디를 기준으로 JOIN 했다.
- 특정 테이블에서 원하는 정보만 불러와 ```JOIN```을 하게 되면 공통되는 부분만 남고 나머지는 출력되지 않는다.(교집합)
- ```JOIN```으로 테이블을 조금 변형하여 가져올 수 있는 점을 어떤 문제에서든 잘 적용할 수 있도록 연습을 많이 해봐야겠다!
 
<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}
