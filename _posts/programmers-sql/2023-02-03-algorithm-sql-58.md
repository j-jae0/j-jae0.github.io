---
title:  "[프로그래머스 SQL] Lv 4. 저자 별 카테고리 별 매출액 집계하기"
layout: single

categories: "Algorithm_SQL"
tags: ["GROUP BY", "JOIN", "SUM"]

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

|Column name|	Type	|Nullable|	Description|
|:----------|:----------|:-------|:------------|
|BOOK_ID|	INTEGER|	FALSE|	도서 ID|
|CATEGORY|	VARCHAR(N)|	FALSE|	카테고리 (경제, 인문, 소설, 생활, 기술)|
|AUTHOR_ID	|INTEGER|	FALSE|	저자 ID|
|PRICE|	INTEGER|	FALSE|	판매가 (원)|
|PUBLISHED_DATE|	DATE|	FALSE|	출판일|

```AUTHOR``` 테이블은 도서의 저자의 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.

|Column name|	Type|	Nullable|	Description|
|:----------|:----------|:-------|:------------|
|AUTHOR_ID|	INTEGER	|FALSE|	저자 ID|
|AUTHOR_NAME|	VARCHAR(N)|	FALSE|	저자명|

```BOOK_SALES``` 테이블은 각 도서의 날짜 별 판매량 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.

|Column name|	Type|	Nullable|	Description|
|:----------|:------|:----------|:-------------|
|BOOK_ID|	INTEGER	|FALSE|	도서 ID|
|SALES_DATE	|DATE|	FALSE|	판매일|
|SALES	|INTEGER|	FALSE	|판매량|

## 문제
```2022년 1월```의 도서 판매 데이터를 기준으로 저자 별, 카테고리 별 매출액(```TOTAL_SALES``` = 판매량 * 판매가) 을 구하여, 저자 ID(```AUTHOR_ID```), 저자명(```AUTHOR_NAME```), 카테고리(```CATEGORY```), 매출액(```SALES```) 리스트를 출력하는 SQL문을 작성해주세요.<br>
결과는 저자 ID를 오름차순으로, 저자 ID가 같다면 카테고리를 내림차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/144856)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT A.AUTHOR_ID, A.AUTHOR_NAME, T1.CATEGORY, 
       SUM(T1.SALES * T1.PRICE) AS TOTAL_SALES
FROM (SELECT BS.BOOK_ID, BS.SALES, B.CATEGORY, B.AUTHOR_ID, B.PRICE 
    FROM (SELECT BOOK_ID, SUM(SALES) AS SALES
          FROM BOOK_SALES
          WHERE DATE_FORMAT(SALES_DATE, "%Y-%m") = "2022-01"
          GROUP BY BOOK_ID
          ORDER BY BOOK_ID) AS BS
    INNER JOIN BOOK AS B ON B.BOOK_ID = BS.BOOK_ID) AS T1
INNER JOIN AUTHOR AS A ON T1.AUTHOR_ID = A.AUTHOR_ID
GROUP BY A.AUTHOR_ID, A.AUTHOR_NAME, T1.CATEGORY
ORDER BY A.AUTHOR_ID, T1.CATEGORY DESC
```

## (2) 코드 리뷰 및 회고
총 3개의 테이블을 JOIN 하여 책 정보(가격, 출판일, 카테고리 등), 저자 정보(저자 ID, 저자명), 판매 정보(책ID별 판매수, 판매일)을 합쳤다.
- INNER JOIN을 한 이유는 NULL값을 처리할 필요가 없었고, 두 테이블에 공통적으로 존재하는 것을 기준으로 합쳤기 때문이다.
- ```BOOK_SALES``` 테이블을 불러올 땐, 2022년 1월에 판매된 데이터만 불러와질 수 있도록 WHERE문에 조건을 넣었다.

### 🤔 문제에서 어려웠던 점
```sql
SELECT A.AUTHOR_ID, A.AUTHOR_NAME, T1.CATEGORY, 
       T1.SALES * T1.PRICE AS TOTAL_SALES
FROM (SELECT BS.BOOK_ID, BS.SALES, B.CATEGORY, B.AUTHOR_ID, B.PRICE 
    FROM (SELECT BOOK_ID, SUM(SALES) AS SALES
          FROM BOOK_SALES
          WHERE DATE_FORMAT(SALES_DATE, "%Y-%m") = "2022-01"
          GROUP BY BOOK_ID
          ORDER BY BOOK_ID) AS BS
    INNER JOIN BOOK AS B ON B.BOOK_ID = BS.BOOK_ID) AS T1
INNER JOIN AUTHOR AS A ON T1.AUTHOR_ID = A.AUTHOR_ID
GROUP BY A.AUTHOR_ID, A.AUTHOR_NAME, T1.CATEGORY
ORDER BY A.AUTHOR_ID, T1.CATEGORY DESC
```
- 위와 같이 코드를 작성했을 때, 정답이 아니라는 결과가 나왔다.
- 처음엔 ```JOIN```이 잘못된건가 생각했지만 ```JOIN```은 내가 원하는대로 잘 되었다.(한줄씩 코드를 작성하여 체크함)
- 이유는 ```GROUP BY``` 때문이었다는 것! ```GROUP BY``` 를 하고 다른 열(```GROUP BY``` 하지 않은 것)을 불러오려면 집계함수를 사용해야 한다. 그게 아니라면 첫 번째 행(대표 행 1개) 만 불러와진다. 는 점을 간과하고 있었다.
- 즉, 카테고리가 '인문'인 것에 책이 두 권이상일 수 있는데 집계함수를 사용하지 않아서 첫 번째 행만 불러와진 것이다.
- ```GROUP BY``` ! ```집계 함수``` ! 기억하자.

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}