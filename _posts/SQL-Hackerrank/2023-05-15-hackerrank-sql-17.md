---
title:  "[해커랭크 SQL] Basic Join 문제풀이 (2)"
layout: single

categories: "Algorithm_SQL"
tags: ["JOIN", "MAX", "SUM", "GROUP BY", "HAVING"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>해커랭크(HackerRank) MySQL, 난이도 MEDIUM 'Contest Leaderboard' 문제 풀이</small>

***

# 1. Contest Leaderboard
You did such a great job helping Julia with her last coding contest challenge that she wants you to work on this one, too!

The total score of a hacker is the sum of their maximum scores for all of the challenges. Write a query to print the hacker_id, name, and total score of the hackers ordered by the descending score. If more than one hacker achieved the same total score, then sort the result by ascending hacker_id. Exclude all hackers with a total score of 0 from your result.

[📍 Contest Leaderboard 문제 보러가기](https://www.hackerrank.com/challenges/contest-leaderboard/problem?isFullScreen=true)

## (1) 테이블 정보
The following tables contain contest data:

**Hackers**: The hacker_id is the id of the hacker, and name is the name of the hacker.

| Column | Type |
|:-------|:-----|
| hacker_id | Integer |
| name | String |

**Submissions**: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, challenge_id is the id of the challenge for which the submission belongs to, and score is the score of the submission.

| Column | Type |
|:-------|:-----|
| submission_id | Integer |
| hacker_id | Integer |
| challenge_id | Integer |
| score | Integer |

## (2) 문제 이해
테이블에는 코딩 콘테스트 도전에 참가한 해커들의 정보(id, 이름, 챌린지id, 제출id, 점수)이 있다. 해커는 여러 챌린지에 도전할 수 있고 챌린지에서 한 개 이상의 점수를 보유할 수 있다. 해커별로 총 점수를 계산하고 점수를 기준으로 내림차순, id를 기준으로 오름차순 정렬한다. <br>
<small>cf. 이때 해커의 총 점수는 챌린지별 최대점수의 합계이다.</small>

## (3) 코드 작성
```sql
SELECT T1.hacker_id, T2.name, SUM(T1.score) AS total_score
FROM (SELECT hacker_id, challenge_id, MAX(score) AS score
      FROM SUBMISSIONS
      GROUP BY hacker_id, challenge_id) AS T1
INNER JOIN HACKERS AS T2 ON T1.hacker_id = T2.hacker_id
GROUP BY T1.hacker_id, T2.name
HAVING total_score > 0
ORDER BY total_score DESC, hacker_id
```

<div style="text-align : center;">
<img src="/assets/images/algorithm/hackerrank_17_1.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (4) 코드 리뷰
우선 SUBMISSIONS 테이블엔 해커의 모든 점수가 기록되어있기 때문에 챌린지 별 최대점수를 불러오기 위해 해커 id, 챌린지 id를 기준으로 그룹화하고 MAX 함수로 점수의 최대점수를 불러왔다. (서브쿼리 T1)<br>
그리고 해커의 이름정보를 불러오기 위해 HACKERS 테이블과 해커 아이디를 기준으로 INNER JOIN했다. 최종 점수는 챌린지별 최대점수의 합이다. 최종 점수를 계산하기 위해 해커의 아이디, 이름을 기준으로 그룹화하고 SUM 함수로 점수의 합을 계산했다.<br>
이렇게 해커별로 총 점수를 구하면 0점을 가진 해커들의 항목이 나오게 되는데 '총 점수가 0인 해커는 제외한다.' 라는 조건이 있기 때문에 HAVING 절에 총 점수가 0보다 크다는 조건을 추가했다. 이렇게 필요한 데이터만 추출하고 총점수를 기준으로 내림차순 정렬, 만약 점수가 같다면 해커 아이디를 기준으로 오름차순 정렬을 해주었다. <br>

문제 한 줄 요약: **EASY 😎**


👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}