---
title:  "[프로그래머스 SQL] Lv 3. 조회수가 가장 많은 중고거래 게시판의 첨부파일 조회하기"
layout: single

categories: "Algorithm_SQL"
tags: ["JOIN", "CONCAT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - String, Date 문제</small>

***

# <span class="half_HL">✔️ 문제 설명</span>
다음은 중고거래 게시판 정보를 담은 ```USED_GOODS_BOARD``` 테이블과 중고거래 게시판 첨부파일 정보를 담은 ```USED_GOODS_FILE``` 테이블입니다.  ```USED_GOODS_BOARD``` 테이블은 다음과 같으며 ```BOARD_ID```, ```WRITER_ID```, ```TITLE```, ```CONTENTS```, ```PRICE```, ```CREATED_DATE```, ```STATUS```, ```VIEWS```은 게시글 ID, 작성자 ID, 게시글 제목, 게시글 내용, 가격, 작성일, 거래상태, 조회수를 의미합니다.

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

```USED_GOODS_FILE``` 테이블은 다음과 같으며 ```FILE_ID```, ```FILE_EXT```, ```FILE_NAME```, ```BOARD_ID```는 각각 파일 ID, 파일 확장자, 파일 이름, 게시글 ID를 의미합니다.

|Column name|	Type|	Nullable|
|:----------|:------|:----------|
|FILE_ID	|VARCHAR(10)|	FALSE|
|FILE_EXT|	VARCHAR(5)|	FALSE|
|FILE_NAME|	VARCHAR(256)|	FALSE|
|BOARD_ID|	VARCHAR(10)	|FALSE|

## 문제
```USED_GOODS_BOARD```와 ```USED_GOODS_FILE``` 테이블에서 조회수가 가장 높은 중고거래 게시물에 대한 첨부파일 경로를 조회하는 SQL문을 작성해주세요. 첨부파일 경로는 FILE ID를 기준으로 내림차순 정렬해주세요. 기본적인 파일경로는 /home/grep/src/ 이며, 게시글 ID를 기준으로 디렉토리가 구분되고, 파일이름은 파일 ID, 파일 이름, 파일 확장자로 구성되도록 출력해주세요. 조회수가 가장 높은 게시물은 하나만 존재합니다.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/164671)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT CONCAT('/home/grep/src/', T2.BOARD_ID, '/', T2.FILE_ID, T2.FILE_NAME, T2.FILE_EXT) AS FILE_PATH
FROM (SELECT * 
      FROM USED_GOODS_BOARD 
      ORDER BY VIEWS DESC 
      LIMIT 1) AS T1
INNER JOIN USED_GOODS_FILE AS T2 ON T1.BOARD_ID = T2.BOARD_ID
ORDER BY T2.FILE_ID DESC
```

## (2) 코드 리뷰 및 회고
- 문제는 조회수가 가장 높은 중고거래 게시물에 대한 첨부파일 경로를 조회하는 것이다.
  - 조회수가 가장 높은 중고거래 게시물 하나만 불러오기 위해 ```FROM```에 서브쿼리를 불러오도록 했다(```LIMIT```문 사용하여 1개 불러옴)
- 게시물에 첨부된 파일 정보를 불러오기 위해 파일 정보가 담긴 테이블과 ```JOIN```으로 결합하였다.
- 파일 경로를 만들기 위해 ```CONCAT``` 함수로 '/home/grep/src/' 와 그 하위 경로를 추가로 결합해주었다.

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}