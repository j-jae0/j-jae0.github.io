---
title:  "[프로그래머스 SQL] Lv 3. 조건에 맞는 사용자 정보 조회하기"
layout: single

categories: "Algorithm_SQL"
tags: ["CONCAT", "COUNT", "JOIN", "LEFT", "MID", "RIGHT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL 고득점 Kit - String, Date 문제</small>

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

```USED_GOODS_USER``` 테이블은 다음과 같으며 ```USER_ID```, ```NICKNAME```, ```CITY```, ```STREET_ADDRESS1```, ```STREET_ADDRESS2```, ```TLNO```는 각각 회원 ID, 닉네임, 시, 도로명 주소, 상세 주소, 전화번호를 의미합니다.

|Column name|	Type|	Nullable|
|:----------|:------|:----------|
|USER_ID	|VARCHAR(50)	|FALSE|
|NICKANME	|VARCHAR(100)	|FALSE|
|CITY	|VARCHAR(100)	|FALSE|
|STREET_ADDRESS1	|VARCHAR(100)	|FALSE|
|STREET_ADDRESS2	|VARCHAR(100)	|TRUE|
|TLNO	|VARCHAR(20)	|FALSE|

## 문제
```USED_GOODS_BOARD```와 ```USED_GOODS_USER``` 테이블에서 중고 거래 게시물을 3건 이상 등록한 사용자의 사용자 ID, 닉네임, 전체주소, 전화번호를 조회하는 SQL문을 작성해주세요. 이때, 전체 주소는 시, 도로명 주소, 상세 주소가 함께 출력되도록 해주시고, 전화번호의 경우 xxx-xxxx-xxxx 같은 형태로 하이픈 문자열(-)을 삽입하여 출력해주세요. 결과는 회원 ID를 기준으로 내림차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/164670)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT U.USER_ID
     , U.NICKNAME
     , CONCAT(U.CITY, ' ', U.STREET_ADDRESS1, ' ', U.STREET_ADDRESS2) AS '전체주소'
     , CONCAT(LEFT(TLNO, 3), '-', MID(TLNO, 4, 4), '-', RIGHT(TLNO, 4)) AS '전화번호'
FROM (SELECT WRITER_ID AS USER_ID
      FROM USED_GOODS_BOARD
      GROUP BY WRITER_ID
      HAVING COUNT(BOARD_ID) >= 3) AS B
INNER JOIN USED_GOODS_USER AS U ON B.USER_ID = U.USER_ID
ORDER BY U.USER_ID DESC
```

## (2) 코드 리뷰 및 회고
- 문제는 중고 거래 게시물을 3건 이상 등록한 사용자의 정보를 출력하는 것이다.
  - 사용자별로 그룹화하여 3건 이상인 사용자 아이디만 불러오도록 서브쿼리 작성
  - 사용자의 정보가 담긴 테이블과 ```JOIN```으로 결합
  - ```USED_GOODS_USER``` 테이블엔 사용자의 주소 정보가 시, 도로명 주소, 상세 주소로 나누어져있어 ```CONCAT```으로 묶어줌
  - 구분자 '-' 없이 저장되어있는 전화번호 정보는 ```CONCAT```과 ```LEFT```, ```MID```, ```RIGHT``` 함수로 구분자를 넣어 새로운 전화번호로 불러옴


전화번호를 불러올 때, ```010``` 대신 ```LEFT(TLNO, 3)```으로 묶어준 이유는 예전엔 011, 016, 019 등으로 다양했기 때문이다. 현재는 010으로 대부분 바뀐것으로 알고있지만 혹시 몰라 LEFT로 처리했다.(옛날 사람🙋🏻‍♀️)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}