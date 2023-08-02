---
title:  "[해커랭크 SQL] Basic Join 문제풀이 (6)"
excerpt: "해커랭크(HackerRank) MySQL, 난이도 MEDIUM 1 문제 풀이"
layout: single

categories: "Algorithm_SQL"
tags: ["NOT IN", "MAX", "COUNT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

***

# Challenges
Julia asked her students to create some coding challenges. Write a query to print the hacker_id, name, and the total number of challenges created by each student. Sort your results by the total number of challenges in descending order. If more than one student created the same number of challenges, then sort the result by hacker_id. If more than one student created the same number of challenges and the count is less than the maximum number of challenges created, then exclude those students from the result.

[🏆🏆🏆 Challenges 문제 보러가기](https://www.hackerrank.com/challenges/challenges/problem?isFullScreen=true)

## (1) 테이블 정보
```Hackers```: The hacker_id is the id of the hacker, and name is the name of the hacker. 

<div style="text-align : center;">
<img src="https://s3.amazonaws.com/hr-challenge-images/19506/1458521004-cb4c077dd3-ScreenShot2016-03-21at6.06.54AM.png" width="30%">
</div>

<br>

```Challenges```: The challenge_id is the id of the challenge, and hacker_id is the id of the student who created the challenge.

<div style="text-align : center;">
<img src="https://s3.amazonaws.com/hr-challenge-images/19506/1458521079-549341d9ec-ScreenShot2016-03-21at6.07.03AM.png" width="30%">
</div>

## (2) 문제 이해
해커 ID, 이름, 총 챌린지 수를 출력하는 쿼리를 작성한다.
1. 한 명 이상의 학생이 같은 수의 도전 과제를 생성하였고 그 수가 생성된 최대 도전 과제 수보다 적은 경우는 제외한다.
2. 총 챌린지 수를 기준으로 내림차순 정렬한다.
3. 두 명 이상의 학생이 동일한 수의 챌린지 수를 가지는 경우 ID로 정렬한다.

## (3) 코드 작성
```sql
SELECT H.hacker_id, H.name, COUNT(C.challenge_id) AS cnt
FROM Hackers AS H
INNER JOIN Challenges AS C ON H.hacker_id = C.hacker_id
GROUP BY H.hacker_id, H.name
HAVING cnt = (SELECT MAX(cnt)
              FROM (SELECT COUNT(*) AS cnt 
                    FROM Challenges 
                    GROUP BY hacker_id) AS T1)
OR cnt NOT IN (SELECT cnt
               FROM (SELECT hacker_id, COUNT(*) AS cnt
                     FROM Challenges
                     GROUP BY hacker_id) AS T2
               GROUP BY cnt
               HAVING COUNT(*) > 1)
ORDER BY cnt DESC, H.hacker_id
```

<div style="text-align : center;">
<img src="/assets/images/sql/hackerrank/hackerrank_mysql_19.png" width="85%">
</div>
<center><small>위 쿼리의 실행 결과</small></center>

<br>

## (4) 코드 리뷰
해커별로 참여한 챌린지를 연결하기 위해 두 테이블(```Hackers```, ```Challenges```)을 INNER JOIN 하였다. 그리고 해커 ID, 해커 이름을 기준으로 그룹화하고 해커별로 참여한 챌린지 수를 구하였다(```cnt```).<br>
문제 이해 중 1번 조건을 만족시키기 위해 HAVING 문에 두 가지 조건식을 작성했다. 첫 번째 조건식은 해커별로 참여한 챌린지 수(```cnt```) 가 MAX 값이다. 그리고 다음 조건식은 cnt가 중복된 경우가 없는 값이다. 두 조건식을 만족시키기 위해 서브쿼리를 만들어주었다.

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}