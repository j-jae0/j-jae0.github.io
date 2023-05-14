---
title:  "[프로그래머스 SQL] Lv 2. 조건에 맞는 도서 리스트 출력하기"
layout: single

categories: "Algorithm_SQL"
tags: ["JOIN", "DATE_FORMAT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small></small>

***

# <span class="half_HL">✔️ 문제 설명</span>
다음은 어느 한 서점에서 판매중인 도서들의 도서 정보(```BOOK```), 저자 정보(```AUTHOR```) 테이블입니다.

```BOOK``` 테이블은 각 도서의 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.

|Column name|	Type|	Nullable|	Description|
|:----------|:-----|:-----------|:------------|
|BOOK_ID|	INTEGER	|FALSE|	도서 ID|
|CATEGORY|	VARCHAR(N)	|FALSE|	카테고리 (경제, 인문, 소설, 생활, 기술)|
|AUTHOR_ID|	INTEGER|	FALSE|	저자 ID|
|PRICE|	INTEGER	|FALSE|	판매가 (원)|
|PUBLISHED_DATE|	DATE|	FALSE	|출판일|
AUTHOR 테이블은 도서의 저자의 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.

|Column name|	Type|	Nullable|	Description|
|:----------|:-----|:-----------|:------------|
|AUTHOR_ID|	INTEGER|	FALSE|	저자 ID|
|AUTHOR_NAME|	VARCHAR(N)|	FALSE|	저자명|

## 문제
'경제' 카테고리에 속하는 도서들의 도서 ID(```BOOK_ID```), 저자명(```AUTHOR_NAME```), 출판일(```PUBLISHED_DATE```) 리스트를 출력하는 SQL문을 작성해주세요.
결과는 출판일을 기준으로 오름차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/144854)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT B.BOOK_ID, A.AUTHOR_NAME, 
       DATE_FORMAT(B.PUBLISHED_DATE, "%Y-%m-%d") AS PUBLISHED_DATE
FROM (SELECT * FROM BOOK WHERE CATEGORY = "경제") AS B
  INNER JOIN AUTHOR AS A ON B.AUTHOR_ID = A.AUTHOR_ID
ORDER BY PUBLISHED_DATE
```

## (2) 코드 리뷰 및 회고
- 두 테이블을 ```JOIN```으로 불러올 때, 책 정보가 담긴 ```BOOK```테이블은 ```WHERE``` 문에 카테고리 조건(```경제```)를 추가해서 불러왔다.
- 그리고 출판일을 불러올 때, 시간 정보를 빼기 위해 ```DATE_FORMAT```으로 연-월-일 형태로 불러왔다.

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}