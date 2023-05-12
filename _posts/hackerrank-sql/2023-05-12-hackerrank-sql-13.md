---
title:  "[해커랭크 SQL] Advanced Select 문제풀이 (4)"
layout: single

categories: "Algorithm_SQL"
tags: ["CASE", "IS NULL", "ANY", "DISTINCT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, MEDIUM 1 문제 풀이</small>

***

# 1. Binary Tree Nodes

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_13_1.png" width="90%">
</div>

[👉 Binary Tree Nodes 문제 보러가기](https://www.hackerrank.com/challenges/binary-search-tree-1/problem?isFullScreen=true)


## (1) 문제 이해
- 이진 트리의 노드 유형을 찾는 문제
- 트리의 형태가 아래와 같을 때, 노드별로 'Root', 'Inner', 'Leaf'로 분류
  - 부모 노드가 없다면 'Root'
  - 부모 노드와 자식 노드가 있다면 'Inner'
  - 부모 노드만 있다면 'Leaf'

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_13_3.png" width="75%">
</div>
<center><small>예시 (제작: PowerPoint)</small></center>

## (2) 코드 작성
```sql
SELECT n,
       CASE
         WHEN p IS NULL THEN 'Root'
         WHEN n = ANY(SELECT DISTINCT p FROM BST) THEN 'Inner' ELSE 'Leaf'
       END AS node
FROM BST
ORDER BY n
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_13_2.png" width="75%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (3) 코드 리뷰
노드를 특정 조건별로 분류를 해야한다. 특히 종류가 3가지라는 점에서 CASE 문을 사용했다. 우선 n은 본인 번호, p는 본인의 부모 노드의 번호를 의미한다. 즉 p가 존재하지 않으면(부모 노드 존재X) 'Root'로 분류할 수 있다. 이를 CASE 문의 첫 번째 WHEN 조건문으로 작성했다. 그 다음으로 부모 노드 목록에 특정 노드가 존재한다면 'Inner'로 분류할 수 있다. 서브쿼리를 만들어서 노드가 부모 노드의 목록에 존재한다면 'Inner', 그 외는 'Leaf'로 분류 될 수 있도록 CASE문을 완성했다. 결과는 n을 기준으로 오름차순 정렬하였다.

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}