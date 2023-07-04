---
title:  "[프로그래머스 SQL] Lv 1. 조건에 부합하는 중고거래 댓글 조회하기"
layout: single

categories: "Algorithm_SQL"
tags: ["JOIN"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - SELECT 문제</small>

***

# <span class="half_HL">✔️ 문제 설명</span>
다음은 중고거래 게시판 정보를 담은 ```USED_GOODS_BOARD``` 테이블과 중고거래 게시판 첨부파일 정보를 담은 ```USED_GOODS_REPLY``` 테이블입니다. ```USED_GOODS_BOARD``` 테이블은 다음과 같으며 ```BOARD_ID```, ```WRITER_ID```, ```TITLE```, ```CONTENTS```, ```PRICE```, ```CREATED_DATE```, ```STATUS```, ```VIEWS```은 게시글 ID, 작성자 ID, 게시글 제목, 게시글 내용, 가격, 작성일, 거래상태, 조회수를 의미합니다.

|Column name|	Type|	Nullable|
|:----------|:------|:----------|
|BOARD_ID|	VARCHAR(5)|	FALSE|
|WRITER_ID|	VARCHAR(50)|	FALSE|
|TITLE|	VARCHAR(100)|	FALSE|
|CONTENTS|	VARCHAR(1000)|	FALSE|
|PRICE|	NUMBER|	FALSE|
|CREATED_DATE|	DATE|	FALSE|
|STATUS|	VARCHAR(10)|	FALSE|
|VIEWS|	NUMBER|	FALSE|

```USED_GOODS_REPLY``` 테이블은 다음과 같으며 ```REPLY_ID```, ```BOARD_ID```, ```WRITER_ID```, ```CONTENTS```, ```CREATED_DATE```는 각각 댓글 ID, 게시글 ID, 작성자 ID, 댓글 내용, 작성일을 의미합니다.

|Column name|	Type|	Nullable|
|:----------|:------|:----------|
|REPLY_ID	|VARCHAR(10)	|FALSE|
|BOARD_ID	|VARCHAR(5)|	FALSE|
|WRITER_ID	|VARCHAR(50)|	FALSE|
|CONTENTS	|VARCHAR(1000)|	TRUE|
|CREATED_DATE	|DATE	|FALSE|

## 문제
```USED_GOODS_BOARD```와 ```USED_GOODS_REPLY``` 테이블에서 2022년 10월에 작성된 게시글 제목, 게시글 ID, 댓글 ID, 댓글 작성자 ID, 댓글 내용, 댓글 작성일을 조회하는 SQL문을 작성해주세요. 결과는 댓글 작성일을 기준으로 오름차순 정렬해주시고, 댓글 작성일이 같다면 게시글 제목을 기준으로 오름차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/164673)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT UGB.TITLE
     , UGB.BOARD_ID
     , UGR.REPLY_ID
     , UGR.WRITER_ID
     , UGR.CONTENTS
     , DATE_FORMAT(UGR.CREATED_DATE, '%Y-%m-%d') AS CREATED_DATE
FROM USED_GOODS_BOARD AS UGB
INNER JOIN USED_GOODS_REPLY AS UGR ON UGB.BOARD_ID = UGR.BOARD_ID
WHERE DATE_FORMAT(UGB.CREATED_DATE, '%Y-%m') = '2022-10'
ORDER BY UGR.CREATED_DATE, UGB.TITLE
```

## (2) 코드 리뷰 및 회고
- 추출해야하는 데이터는 2022년 10월에 작성된 게시글 제목, 게시글 ID 등의 컬럼이다.
- 게시물에 달린 댓글 정보도 불러와야하기 때문에 JOIN으로 두 테이블(게시물 정보 테이블, 게시물에 달린 댓글 정보 테이블)을 결합하였다.
- 이때 2022년 10월에 작성된 게시글 정보만 불러오기 위해 WHERE 절에 조건문을 작성했다. 
- 결과는 댓글 작성일과 게시글 제목을 기준으로 정렬하여 불러오도록 했다.

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}