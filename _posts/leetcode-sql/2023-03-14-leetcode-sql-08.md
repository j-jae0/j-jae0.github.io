---
title:  "[리트코드 SQL] Day 7. Function"
layout: single

categories: "Algorithm_SQL"
tags: [""]

toc: true
toc_sticky: true
toc_label : "목차"
toc_icon: "bars"

published: false
---

<small>SQL I : Day 7 Function 3문제 풀이</small>

***

# <span class="half_HL">1141. User Activity for the Past 30 Days I</span>

## (1) 코드 작성
```sql
SELECT activity_date AS day, COUNT(DISTINCT USER_ID) AS active_users
FROM Activity
WHERE DATEDIFF('2019-07-27', activity_date) < 30 AND activity_date <= '2019-07-27'
GROUP BY activity_date
HAVING active_users > 0
```

## (2) 코드 리뷰 및 회고
- 
- [👉 문제 보러가기](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1693. Daily Leads and Partners</span>

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
- 
- [👉 문제 보러가기](https://leetcode.com/problems/daily-leads-and-partners/?envType=study-plan&id=sql-i)

<br>

# <span class="half_HL">1729. Find Followers Count</span>

## (1) 코드 작성
```sql
SELECT user_id
     , COUNT(DISTINCT follower_id) AS followers_count
FROM Followers
GROUP BY user_id
```

## (2) 코드 리뷰 및 회고
- 
- [👉 문제 보러가기](https://leetcode.com/problems/find-followers-count/?envType=study-plan&id=sql-i)

<br>

👩🏻‍💻개인 공부 기록용 블로그입니다
<br>오류나 틀린 부분이 있을 경우 댓글 혹은 메일로 따끔하게 지적해주시면 감사하겠습니다.
{: .notice}