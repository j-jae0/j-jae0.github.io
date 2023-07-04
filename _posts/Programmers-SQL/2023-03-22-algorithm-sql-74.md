---
title:  "[프로그래머스 SQL] Lv 3. 조건에 맞는 사용자와 총 거래금액 조회하기"
layout: single

categories: "Algorithm_SQL"
tags: ["SUM", "HAVING", "JOIN"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - GROUP BY 문제</small>

***

# <span class="half_HL">✔️ 문제 설명</span>
다음은 중고 거래 게시판 정보를 담은 ```USED_GOODS_BOARD``` 테이블과 중고 거래 게시판 첨부파일 정보를 담은 ```USED_GOODS_FILE``` 테이블입니다. ```USED_GOODS_BOARD``` 테이블은 다음과 같으며 ```BOARD_ID```, ```WRITER_ID```, ```TITLE```, ```CONTENTS```, ```PRICE```, ```CREATED_DATE```, ```STATUS```, ```VIEWS```는 게시글 ID, 작성자 ID, 게시글 제목, 게시글 내용, 가격, 작성일, 거래상태, 조회수를 의미합니다.

|Column name|	Type|	Nullable|
|:----------|:------|:----------|
|BOARD_ID	|VARCHAR(5)|	FALSE|
|WRITER_ID	|VARCHAR(50)|	FALSE|
|TITLE	|VARCHAR(100)|	FALSE|
|CONTENTS	|VARCHAR(1000)|	FALSE|
|PRICE|	NUMBER|	FALSE|
|CREATED_DATE	|DATE|	FALSE|
|STATUS	|VARCHAR(10)|	FALSE|
|VIEWS	|NUMBER|	FALSE|

```USED_GOODS_USER``` 테이블은 다음과 같으며 ```USER_ID```, ```NICKNAME```, ```CITY```, ```STREET_ADDRESS1```, ```STREET_ADDRESS2```, ```TLNO```는 각각 회원 ID, 닉네임, 시, 도로명 주소, 상세 주소, 전화번호를 를 의미합니다.

|Column name|	Type|	Nullable|
|:----------|:------|:----------|
|USER_ID	|VARCHAR(50)	|FALSE|
|NICKANME	|VARCHAR(100)	|FALSE|
|CITY	|VARCHAR(100)	|FALSE|
|STREET_ADDRESS1	|VARCHAR(100)	|FALSE|
|STREET_ADDRESS2	|VARCHAR(100)	|TRUE|
|TLNO	|VARCHAR(20)	|FALSE|

## 문제
```USED_GOODS_BOARD```와 ```USED_GOODS_USER``` 테이블에서 완료된 중고 거래의 총금액이 70만 원 이상인 사람의 회원 ID, 닉네임, 총거래금액을 조회하는 SQL문을 작성해주세요. 결과는 총거래금액을 기준으로 오름차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/164668)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT T1.USER_ID, T2.NICKNAME, T1.TOTAL_SALES
FROM (SELECT WRITER_ID AS USER_ID
           , SUM(PRICE) AS TOTAL_SALES
      FROM USED_GOODS_BOARD 
      WHERE STATUS = 'DONE' 
      GROUP BY WRITER_ID 
      HAVING SUM(PRICE) >= 700000) AS T1
INNER JOIN USED_GOODS_USER AS T2 ON T1.USER_ID = T2.USER_ID
ORDER BY T1.TOTAL_SALES
```

## (2) 코드 리뷰 및 회고
- 문제는 완료된 중고 거래의 총금액이 70만원 이상인 사람의 정보를 불러오는 것이다.
  - 중고 거래 게시판 정보가 담긴 USED_GOODS_BOARD 를 서브쿼리로 불러온다.
    - 거래가 완료된 조건을 WHERE 문에 작성
    - 작성자를 기준으로 그룹화하고 HAVING 문에 금액이 70만원 이상 조건 추가
  - 작성자 정보가 담긴 테이블과 사용자 아이디를 기준으로 JOIN으로 결합한다.
  - 총 거래 금액을 기준으로 오름차순 정렬했다.

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}