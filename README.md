# Reddit
 This project involves querying a database with tables for users, posts and subreddits to identify the useful information for the company. 
select * from users
limit 3;
select * from posts
limit 3;
select * from subreddits
limit 3;

--The primery key for all tables is id (is a field to uniquely identify data from a table) foreign id subreddit_id
select count(*) as subreddits_count 
from subreddits; 

-- What user has the higher score
select max(score) as 'Users Max Score' from users;

--What post has the higher score 
select max(score) as 'Posts Max Score' from posts; 

--What are the top 5 subreddits with the highest subscriber_count ? 
select id, subscriber_count
from subreddits
order by 2 desc
limit 5; 


-- left join to figure it out how many post each user has made 
select users.id, users.username, count(posts.id) as 'number of posts'
from users
left join posts
on users.id = posts.user_id
Group by 1
order by 3 desc
limit 3;

-- Users that are active, meaning the one who have made posts
select *
from posts 
join users 
on posts.user_id = users.id
limit 3; 

-- Add new posts made 
select * from posts 
union 
select * from posts2
limit 3; 

-- which subreddits have the most popular posts, score > 5000. 
WITH popular_posts AS (
  SELECT *
  FROM posts
  WHERE score >= 5000
)
SELECT subreddits.name, popular_posts.title, popular_posts.score
FROM subreddits
INNER JOIN popular_posts
  ON subreddits.id = popular_posts.subreddit_id
ORDER BY popular_posts.score DESC
limit 3;

-- highest score post for ecah subredit 
select posts.title, subreddits.name as 'subreddit_name', max(posts.score) as 'highest_score'
from posts
inner join subreddits
on posts.subreddit_id = subreddits.id 
Group by subreddits.id
limit 3;

--avg of all posts for each reddit 
select posts.title, subreddits.name as 'subreddit_name', avg(posts.score) as 'avg score'
from posts
inner join subreddits
on posts.subreddit_id = subreddits.id 
Group by subreddits.id
limit 3;



