---
title:  "[프로그래머스 SQL] Lv 3. 카테고리 별 도서 판매량 집계하기"
layout: single

categories: "Algorithm_SQL"
tags: ["JOIN", "SUM", "DATE_FORMAT", "GROUP BY", "ORDER BY"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<br>

***

# <span class="half_HL">✔️ 문제 설명</span>
다음은 어느 한 서점에서 판매중인 도서들의 도서 정보(```BOOK```), 판매 정보(```BOOK_SALES```) 테이블입니다.

```BOOK``` 테이블은 각 도서의 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.

|Column name|	Type|	Nullable|	Description|
|:---|:--|:--|:--|
|BOOK_ID|	INTEGER|	FALSE|	도서 ID|
|CATEGORY|	VARCHAR(N)|	FALSE	|카테고리 (경제, 인문, 소설, 생활, 기술)|
|AUTHOR_ID|	INTEGER	|FALSE|	저자 ID|
|PRICE|	INTEGER	|FALSE|	판매가 (원)|
|PUBLISHED_DATE|	DATE|	FALSE|	출판일|

```BOOK_SALES``` 테이블은 각 도서의 날짜 별 판매량 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.

|Column name|	Type|	Nullable|	Description|
|:---|:--|:--|:--|
|BOOK_ID|	INTEGER	|FALSE|	도서 ID|
|SALES_DATE|	DATE|	FALSE|	판매일|
|SALES|	INTEGER	|FALSE	|판매량|

## 문제
```2022년 1월```의 카테고리 별 도서 판매량을 합산하고, 카테고리(```CATEGORY```), 총 판매량(```TOTAL_SALES```) 리스트를 출력하는 SQL문을 작성해주세요.
결과는 카테고리명을 기준으로 오름차순 정렬해주세요.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/144855)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT CATEGORY, SUM(SALES) AS TOTAL_SALES
FROM (SELECT BOOK_ID, SUM(SALES) AS SALES
      FROM BOOK_SALES
      WHERE DATE_FORMAT(SALES_DATE, "%Y-%m") = "2022-01"
      GROUP BY BOOK_ID) AS BS
      INNER JOIN BOOK AS B ON B.BOOK_ID = BS.BOOK_ID
GROUP BY CATEGORY
ORDER BY CATEGORY
```

## (2) 코드 리뷰 및 회고
문제를 먼저 파악해보면, 아래와 같다.
1. 2022년 1월에 판매된 책 정보를 가져온다.
2. 카테고리별로 총 판매량을 구한다.
<br>
- 위 사항들을 만족하기 위해 우선 ```BOOK_SALES``` 테이블에서 ```SALES_DATE```가 2022년 1월인 데이터를 책 ID로 그룹화하여 판매량을 구한 것을 ```BS```(별칭)로 불러왔다.
- 그리고 ```BOOK``` 테이블을 ```B```로 별칭을 정하고 **책 ID**를 기준으로 ```INNER JOIN``` 하여 아래와 같이 불러올 수 있도록 했다. 
- 
- (아래는 위 과정을 설명하기 위한 예시)

**BS 테이블**
|BOOK_ID|SALES|
|:------|:----|
|001|3|
|002|2|
|003|1|

**B 테이블**
|BOOK_ID|CATEGORY|AUTHOR_ID|PRICE|PUBLISHED_DATE|
|:------|:----|:------|:----|:------|
|001|인문|a001|12000|2021-02-05|
|002|인문|a002|15000|2022-01-01|
|003|과학|a003|21000|2021-05-24|

**BS와 B, INNER JOIN 후**
|BOOK_ID|SALES|CATEGORY|AUTHOR_ID|PRICE|PUBLISHED_DATE|
|:------|:----|:----|:------|:----|:------|
|001|3|인문|a001|12000|2021-02-05|
|002|2|인문|a002|15000|2022-01-01|
|003|1|과학|a003|21000|2021-05-24|

**CATEGORY로 그룹화하고 카테고리, 총판매량만 출력**
|카테고리|총 판매량|
|:-----|:------|
|인문|5|
|과학|1|

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}
