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
