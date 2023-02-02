---
title:  "[프로그래머스 SQL] Lv 4. 우유와 요거트가 담긴 장바구니"
layout: single

categories: "Algorithm_SQL"
tags: ["GROUP_CONCAT", "LIKE", "GROUP BY"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>오류 해결🌞(Every derived table must have its own alias)</small><br>
<small>Summer/Winter Coding(2019)</small>

***

# <span class="half_HL">✔️ 문제 설명</span>
```CART_PRODUCTS``` 테이블은 장바구니에 담긴 상품 정보를 담은 테이블입니다. ```CART_PRODUCTS``` 테이블의 구조는 다음과 같으며, ```ID```, ```CART_ID```, ```NAME```, ```PRICE```는 각각 테이블의 아이디, 장바구니의 아이디, 상품 종류, 가격을 나타냅니다.

|NAME|	TYPE|
|:---|:-----|
|ID|	INT|
|CART_ID|	INT|
|NAME|	VARCHAR|
|PRICE|	INT|

## 문제
데이터 분석 팀에서는 우유(```Milk```)와 요거트(```Yogurt```)를 동시에 구입한 장바구니가 있는지 알아보려 합니다. 우유와 요거트를 동시에 구입한 장바구니의 아이디를 조회하는 SQL 문을 작성해주세요. 이때 결과는 장바구니의 아이디 순으로 나와야 합니다.
<br>[👉 문제 보러가기](https://school.programmers.co.kr/learn/courses/30/lessons/62284)

<br>

# <span class="half_HL">✔️ 문제 풀이</span>
## (1) 코드 작성
```sql
SELECT CART_ID
FROM (SELECT CART_ID, GROUP_CONCAT(NAME) AS NAME
      FROM CART_PRODUCTS
      WHERE NAME LIKE "Milk" OR NAME LIKE "Yogurt"
      GROUP BY CART_ID) AS C
WHERE NAME LIKE "%Milk%" AND NAME LIKE "%Yogurt%"
ORDER BY CART_ID # 넣지않아도 정답처리 됨
```

## (2) 코드 리뷰 및 회고
- 문제는 유저의 장바구니에 요거트와 우유가 들어가있는 경우를 불러오는 것이다.
- CART_PRODUCTS 테이블에는 한 장바구니 ID에 들어가있는 품목이 행으로 구성되어 있다.(아래와 같음)

```CART_PRODUCTS``` 테이블 구조

|ID|CART_ID|NAME|PRICE|
|:--|:-----|:---|:----|
|101|00101|Milk|1500|
|102|00101|Yogurt|4400|
|301|00103|Milk|1500|
|302|00103|Milk|1500|
|303|00103|SODA|3000|

- 요거트와 우유 두 품목이 모두 포함된 장바구니 데이터를 불러와야하기 때문에 FROM으로 테이블을 불러올 때, ```SELECT-FROM-WHERE-GROUP BY``` 구문으로 테이블을 조금 변경하여 가져왔다.
- 변경 사항은 WHERE문에 우유 또는 요거트가 포함된 것을 불러오고 장바구니 아이디로 그룹화하였다.
- 이렇게 하면 장바구니별로 우유 또는 요거트가 하나라도 포함된 장바구니 ID를 불러올 수 있다. 그리고 ```GROUP_CONCAT``` 으로 장바구니 ID별 품목을 ```,```을 구분자로 묶어주었다.
- 마지막으로 전체 품목(GROUP_CONCAT으로 묶은 NAME)에 요거트와 우유가 모두 되어야 한다는 조건을 ```WHERE```에 추가했다.

### 💡 AND가 아닌 OR을 사용한 이유
```sql
FROM (SELECT CART_ID, GROUP_CONCAT(NAME) AS NAME
      FROM CART_PRODUCTS
      WHERE NAME LIKE "Milk" OR NAME LIKE "Yogurt"
      GROUP BY CART_ID) AS C
```
정답 코드에서 FROM으로 테이블을 조금 수정하여 가져올 때, WHERE문에 AND가 아닌 OR을 불러온 이유는 아래와 같다.
- raw 데이터 구조를 보면 장바구니에 포함된 항목들이 하나의 행(raw)로 구성된다. 즉, NAME(품목)을 AND로 불러온다면 아무 데이터도 불러올 수 없다.(아래와 같음)

```CART_PRODUCTS``` 테이블 구조

|ID|CART_ID|NAME|PRICE|
|:--|:-----|:---|:----|
|101|00101|Milk|1500|
|102|00101|Yogurt|4400|
|301|00103|Milk|1500|
|302|00103|Milk|1500|
|303|00103|SODA|3000|

```sql
-- OR로 불러올 경우
SELECT CART_ID
FROM CART_PRODUCTS
WHERE NAME LIKE "Milk" OR NAME LIKE "Yogurt"
```

|ID|CART_ID|NAME|PRICE|
|:--|:-----|:---|:----|
|101|00101|Milk|1500|
|102|00101|Yogurt|4400|
|301|00103|Milk|1500|
|302|00103|Milk|1500|

```sql
-- AND로 불러올 경우
SELECT CART_ID
FROM CART_PRODUCTS
WHERE NAME LIKE "Milk" AND NAME LIKE "Yogurt"
```

|ID|CART_ID|NAME|PRICE|
|:--|:-----|:---|:----|

- 위와 같은 이유로 AND가 아닌 OR를 사용했다.

## 🌞 에러사항 공유
```sql
SELECT CART_ID
FROM (SELECT CART_ID, GROUP_CONCAT(NAME) AS NAME
      FROM CART_PRODUCTS
      WHERE NAME LIKE "Milk" OR NAME LIKE "Yogurt"
      GROUP BY CART_ID)
```

**SQL 실행 중 오류가 발생하였습니다.**<br>
Every derived table must have its own alias

- 위와 같은 메시지가 발생하는 이유는 서브쿼리에 Alias를 주지 않았기 때문이다.
- 처음 오류 메시지를 보았을 때 서브쿼리를 불러올 수 없는건가? 생각했지만 MySQL에선 Alias를 줘야 불러올 수 있다고 한다!(오라클에서는 X)
- Python, Pandas로 데이터 프레임을 만들고 또 데이터 프레임을 다른 변수에 저장하여 활용할 때 copy 함수를 사용하라는 warning message가 뜰 때가 있는데 그거와 비슷하다는 생각이 들었다.
- 기존의 테이블을 수정하여 새로운 df로 활용할 때, Alias(별칭)을 꼭 주자!

```sql
SELECT CART_ID
FROM (SELECT CART_ID, GROUP_CONCAT(NAME) AS NAME
      FROM CART_PRODUCTS
      WHERE NAME LIKE "Milk" OR NAME LIKE "Yogurt"
      GROUP BY CART_ID) AS C # AS 없이 C라고만 작성해도 됨
```
Note. 에러가 발생한 코드를 수정하면 위와 같다!(별칭 추가)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}
