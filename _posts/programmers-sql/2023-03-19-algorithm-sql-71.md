---
title:  "[프로그래머스 SQL] Lv 2. 조건에 부합하는 중고거래 상태 조회하기"
layout: single

categories: "Algorithm_SQL"
tags: ["CASE"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - String, Date 문제</small>

***

# <span class="half_HL">✔️ 문제 설명</span>
다음은 중고거래 게시판 정보를 담은 ```USED_GOODS_BOARD``` 테이블입니다. ```USED_GOODS_BOARD``` 테이블은 다음과 같으며 ```BOARD_ID```, ```WRITER_ID```, ```TITLE```, ```CONTENTS```, ```PRICE```, ```CREATED_DATE```, ```STATUS```, ```VIEWS```은 게시글 ID, 작성자 ID, 게시글 제목, 게시글 내용, 가격, 작성일, 거래상태, 조회수를 의미합니다.

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

## 문제
```USED_GOODS_BOARD``` 테이블에서 2022년 10월 5일에 등록된 중고거래 게시물의 게시글 ID, 작성자 ID, 게시글 제목, 가격, 거래상태를 조회하는 SQL문을 작성해주세요. 거래상태가 SALE 이면 판매중, RESERVED이면 예약중, DONE이면 거래완료 분류하여 출력해주시고, 결과는 게시글 ID를 기준으로 내림차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/164672)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT BOARD_ID, WRITER_ID, TITLE, PRICE,
       CASE 
         WHEN STATUS = 'SALE' THEN '판매중'
         WHEN STATUS = 'RESERVED' THEN '예약중' 
         ELSE '거래완료'
       END AS STATUS
FROM USED_GOODS_BOARD
WHERE DATE_FORMAT(CREATED_DATE, '%Y-%m-%d') = '2022-10-05'
ORDER BY BOARD_ID DESC
```

## (2) 코드 리뷰 및 회고
- 해당 문제는 2022년 10월 5일에 등록된 중고거래 게시물의 정보를 조회하는 것이다.
- 이때, 거래 상태별로 특정 키워드로 분류하여 추출해야한다.
  - 상태가 SALE, RESERVED, 그외로 총 3가지 케이스에 대해 분류해줘야하기 때문에 CASE문을 사용했다.

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}