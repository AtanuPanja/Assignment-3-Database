
1. Fetch all users name from database

Answer
```sql
SELECT user_name from Users;
```

2. Fetch all tweets of user by user id most recent tweets first

Answer
```sql
SELECT user_id, message
FROM Tweets
WHERE user_id = 1
ORDER BY created_date DESC;
```

3. Fetch like count of particular tweet by tweet id.

Answer
```sql
SELECT tweet_id, COUNT(tweet_id) AS no_of_likes
FROM Likes
WHERE tweet_id = 1;
```

4. Fetch retweet count of particular tweet by tweet id


Answer
```sql
SELECT original_tweet_id, COUNT(original_tweet_id) 
AS no_of_retweets
FROM Retweets
WHERE original_tweet_id = 1;
```


5. Fetch comment count of particular tweet by tweet id.

Answer
```sql
SELECT tweet_id, COUNT(parent_tweet_id) AS no_of_comments
FROM Tweets
WHERE tweet_id = 3;
```

6. Fetch all user's name who have retweeted particular tweet by tweet id.

Answer
```sql
SELECT rt.original_tweet_id, u.user_name AS user_who_retweeted
FROM Retweets AS rt
INNER JOIN Users as u
ON rt.user_id = u.user_id
WHERE rt.original_tweet_id = 1;
```


7. Fetch all commented tweet's content for particular tweet by tweet id.

Answer
```sql
SELECT parent_tweet_id, message AS comment
FROM Tweets
WHERE parent_tweet_id = 2;
```

8. Fetch user's timeline (All tweets from users whom I am following with tweet content and user name who has tweeted it)

Answer
```sql
-- find all users whom I am following

-- SELECT user_name 
-- FROM Users 
-- WHERE user_id = (
-- 	SELECT following_id 
--     FROM Following
--     WHERE follower_id = 2
-- );

-- now find the tweets of those users
SELECT u.user_name AS users_following, t.message, t.created_date 
FROM Tweets AS t
INNER JOIN Users AS u
ON u.user_id = t.user_id
WHERE u.user_id = (
	SELECT following_id 
    FROM Following
    WHERE follower_id = 1
)
ORDER BY t.created_date DESC;
```