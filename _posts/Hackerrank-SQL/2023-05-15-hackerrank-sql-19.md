---
title:  "[해커랭크 SQL] Basic Join 문제풀이 (4)"
layout: single

categories: "Algorithm_SQL"
tags: ["🌞", "JOIN", "GROUP BY", "HAVING", "COUNT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 MEDIUM 1 문제 풀이</small>

***

# 1. Top Competitors
Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge. Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.

[📍 Top Competitors 문제 보러가기](https://www.hackerrank.com/challenges/full-score/problem?isFullScreen=true)

## (1) 테이블 정보
The following tables contain contest data:

**Hackers**: The hacker_id is the id of the hacker, and name is the name of the hacker.

| Column | Type |
|:-------|:-----|
| hacker_id | Integer |
| name | String |

**Difficulty**: The difficult_level is the level of difficulty of the challenge, and score is the score of the challenge for the difficulty level.

| Column | Type |
|:-------|:-----|
| difficulty_level | Integer |
| score | Integer |

**Challenges**: The challenge_id is the id of the challenge, the hacker_id is the id of the hacker who created the challenge, and difficulty_level is the level of difficulty of the challenge.

| Column | Type |
|:-------|:-----|
| challenge_id | Integer |
| hacker_id | Integer |
| difficulty_level | Integer |

**Submissions**: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, challenge_id is the id of the challenge for which the submission belongs to, and score is the score of the submission.

| Column | Type |
|:-------|:-----|
| submission_id | Integer |
| hacker_id | Integer |
| challenge_id | Integer |
| score | Integer |

## (2) 문제 이해
챌린지에서 만점을 두 번 이상 받은 해커의 아이디와 이름을 출력하는 문제이다. 챌린지에서 만점을 받은 횟수를 기준으로 내림차순 하고, 만약 챌린지에서 만점을 받은 횟수가 동일한 해커가 존재한다면 아이디를 기준으로 오름차순 정렬한다.

## (3) 코드 작성
```sql
SELECT H.hacker_id, H.name
FROM HACKERS AS H
INNER JOIN SUBMISSIONS AS S ON H.hacker_id = S.hacker_id
INNER JOIN CHALLENGES AS C ON S.challenge_id = C.challenge_id
INNER JOIN DIFFICULTY AS D ON C.difficulty_level = D.difficulty_level
WHERE S.score = D.score
GROUP BY H.hacker_id, H.name
HAVING COUNT(*) >= 2
ORDER BY COUNT(*) DESC, H.hacker_id
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_19_1.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (4) 코드 리뷰
- 총 네 개의 테이블을 이용해야 원하는 결과를 불러올 수 있다.
- 테이블은 모두 INNER JOIN으로 결합해주었다.(JOIN과 같은 기능)
- 네 개의 테이블을 연결하고 만점을 받은 횟수를 구해야하기 때문에 획득한 점수가 만점기준의 점수와 같다는 조건을 WHERE 절에 넣었다.
- 해커의 아이디와 이름을 기준으로 그룹화하고 만점을 받은 횟수를 구하기 위해 COUNT 함수를 사용했다.
- '만점을 두 번 이상 받은 해커의 정보'를 불러오기 위해 HAVING 문에 조건식을 추가했다.
- 정렬은 COUNT(*): 만점을 받은 횟수 를 기준으로 내림차순 하고 두번째 정렬 기준으로 해커의 아이디를 넣었다.
- EASY 😎

## 🌞 실패 코드 공유
```sql
SELECT H.hacker_id, H.name
FROM HACKERS AS H
INNER JOIN SUBMISSIONS AS S ON H.hacker_id = S.hacker_id
INNER JOIN CHALLENGES AS C ON S.hacker_id = C.hacker_id AND S.challenge_id = C.challenge_id
INNER JOIN DIFFICULTY AS D ON C.difficulty_level = D.difficulty_level
WHERE S.score = D.score
GROUP BY H.hacker_id, H.name
HAVING COUNT(*) >= 2
ORDER BY COUNT(*) DESC, H.hacker_id
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_19_2.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

실패 코드를 보면, Challenges 테이블을 JOIN 할 때 연결 기준을 해커의 아이디, 챌린지 아이디 두 개가 만족해야함을 넣었다. 그런데 계속 결과가 없다는 wrong sign이 떴고 예제의 테이블 구조를 다시 확인해 보고 이유를 알 수 있었다. 챌린지 테이블에 구성되어있는 챌린지 아이디, 해커 아이디, 난이도 중에서 해커 아이디 값이 맞는 게 없다는 것이었다.(해커 아이디값 없는게 많음) 그래서 연결 조건에 챌린지 아이디만 넣었더니 성공 sign이 떴다. 테이블을 만들 때 오류가 난것으로 보인다. 

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}