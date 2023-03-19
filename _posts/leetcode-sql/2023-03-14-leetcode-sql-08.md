---
title:  "[리트코드 SQL] Day 7. Function"
layout: single

categories: "Algorithm_SQL"
tags: ["DATEDIFF", "COUNT", "DISTINCT"]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"
---

<small>SQL I : Day 7 Function 3문제 풀이</small>

***

# <span class="half_HL">1141. User Activity for the Past 30 Days I</span>
2019-07-27(포함)까지 30일 동안 일일 활성 사용자 수를 찾는 SQL 쿼리를 작성하시오.<br>
테이블: ```Activity```

| Column Name   | Type    |
|:--------------|:--------|
| user_id       | int     |
| session_id    | int     |
| activity_date | date    |
| activity_type | enum    |

## (1) 코드 작성
```sql
SELECT activity_date AS day, COUNT(DISTINCT USER_ID) AS active_users
FROM Activity
WHERE DATEDIFF('2019-07-27', activity_date) < 30 AND activity_date <= '2019-07-27'
GROUP BY activity_date
HAVING active_users > 0
```

## (2) 코드 리뷰 및 회고
- 문제는 2019-07-27일을 포함하여 한 달동안 서비스를 이용한 고객 수를 일자별로 찾는 것이다.
- 2019-07-27을 기준으로 30일 이내에 들어왔다는 조건을 추가하기 위해 ```DATEDIFF``` 함수를 사용했고 2019-07-27 이후에 들어온 유저의 기록은 고려되지 않도록 또 다른 조건식으로 추가해주었다.
- 그 후 날짜별로 몇명의 유저가 들어왔는지 확인하기 위해 ```GROUP BY``` 로 날짜를 그룹화했고 ```USER_ID```의 중복을 제거하여 유저 수를 ```active_users```로 불러왔다. 
- 일자별로 유저수가 0인 행은 불러오지 않도록 ```HAVING``` 문을 사용했다.
- [👉 문제 보러가기](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1693. Daily Leads and Partners</span>
각 ```date_id``` 및 ```make_name```에 대해 고유한 ```lead_id``` 및 고유한 ```partner_id```의 수를 반환하는 SQL 쿼리를 작성하시오.<br>
테이블: ```DailySales```

| Column Name | Type    |
|:------------|:--------|
| date_id     | date    |
| make_name   | varchar |
| lead_id     | int     |
| partner_id  | int     |

## (1) 코드 작성
```sql
SELECT date_id
     , make_name
     , COUNT(DISTINCT lead_id) AS unique_leads
     , COUNT(DISTINCT partner_id) AS unique_partners
FROM DailySales
GROUP BY date_id, make_name
```

## (2) 코드 리뷰 및 회고
- 문제는 날짜와 회사명에 대해 고유한 lead와 고유한 partner 수를 구하는 것이다.
- 문제를 만족하기 위해 날짜와 회사명을 기준으로 그룹화하고 ```SELECT``` 문에서 lead와 partner를 ```DISTINCT```로 중복값을 제거하여 수를 세어 불러왔다. 
- [👉 문제 보러가기](https://leetcode.com/problems/daily-leads-and-partners/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1729. Find Followers Count</span>
각 사용자에 대해 팔로워 수를 반환하는 SQL 쿼리를 작성하시오. ```user_id```로 정렬된 결과 테이블을 오름차순으로 반환합니다.<br>
테이블: ```Followers```

| Column Name | Type |
|:------------|:-----|
| user_id     | int  |
| follower_id | int  |

## (1) 코드 작성
```sql
SELECT user_id
     , COUNT(follower_id) AS followers_count
FROM Followers
GROUP BY user_id
ORDER BY user_id
```

## (2) 코드 리뷰 및 회고
- 문제는 유저별로 팔로워 수를 반환하는 것으로 한 유저에 대해 팔로워하는 사람의 수를 구하는 것이다.
- 유저 아이디별로 그룹화를 하고 집계함수 ```COUNT``` 로 팔로워의 수를 불러왔다.
- 그리고 유저 아이디를 기준으로 오름차순 정렬해 주었다.
- [👉 문제 보러가기](https://leetcode.com/problems/find-followers-count/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}