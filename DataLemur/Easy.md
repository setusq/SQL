__[Histogram of Tweets [Twitter SQL Interview Question]](https://datalemur.com/questions/sql-histogram-tweets)__
> Company: Twitter
```sql
SELECT tweet_bucket, COUNT(*) as users_num
FROM
(SELECT user_id, COUNT(*) as tweet_bucket  FROM tweets
WHERE tweet_date BETWEEN '01/01/2022' AND '12/31/2022'
GROUP BY user_id) a
GROUP BY tweet_bucket
```
__[Data Science Skills [LinkedIn SQL Interview Question]](https://datalemur.com/questions/matching-skills)__
> Company: LinkedLn
```sql
SELECT candidate_id FROM candidates
WHERE skill = 'Python'
OR skill = 'Tableau'
OR skill = 'PostgreSQL'
GROUP BY candidate_id
HAVING count(*) = 3
```
[__Page With No Likes [Facebook SQL Interview Question]](https://datalemur.com/questions/sql-page-with-no-likes)__
> Company: Facebook
```sql
SELECT p.page_id FROM pages p
LEFT JOIN page_likes l 
ON p.page_id = l.page_id
WHERE l.page_id is null
```
__[Unfinished Parts [Tesla SQL Interview Question]](https://datalemur.com/questions/tesla-unfinished-parts)__
> Company: Tesla
```sql
SELECT part, assembly_step FROM parts_assembly
WHERE finish_date IS NULL
```

__[Laptop vs. Mobile Viewership [New York Times SQL Interview Question]](https://datalemur.com/questions/laptop-mobile-viewership)__
> Company: New York Times
```sql
SELECT SUM(CASE WHEN device_type = 'laptop' THEN 1 ELSE 0 END) as laptop_views,
  SUM(CASE WHEN device_type = 'phone' OR device_type = 'tablet'  THEN 1 ELSE 0 END) as mobile_views
FROM viewership;
```
__[Average Post Hiatus (Part 1) [Facebook SQL Interview Question]](https://datalemur.com/questions/sql-average-post-hiatus-1)__
> Company: Facebook
```sql
SELECT user_id, DATE_PART('day', MAX(post_date) - MIN(post_date)) as days_between FROM posts
WHERE post_date BETWEEN '01-01-2021' AND '12-31-2021'
GROUP BY user_id
HAVING DATE_PART('day', MAX(post_date) - MIN(post_date)) <> 0
```

__[Teams Power Users [Microsoft SQL Interview Question]](https://datalemur.com/questions/teams-power-users)__
> Company: Microsift
```sql
SELECT sender_id, count(*) as message_count FROM messages
WHERE sent_date BETWEEN '08-01-2022' AND '08-31-2022'
GROUP BY sender_id
ORDER BY count(*) DESC
LIMIT 2
```
