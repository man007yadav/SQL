`Manoj Yadav` | `SQL Problems Collection`

<!-- MarkdownTOC -->

- [Comments I](#comments-i)
  - [Calculate the average comments for the users with >= 2 posts, and `each` post has comments greater or equal to 40](#calculate-the-average-comments-for-the-users-with--2-posts-and-each-post-has-comments-greater-or-equal-to-40)
- [Article Views](#article-views)
  - [How many article authors have never viewed their own article?](#how-many-article-authors-have-never-viewed-their-own-article)
  - [How many members viewed more than one articles on 2017-08-01](#how-many-members-viewed-more-than-one-articles-on-2017-08-01)
<!-- /MarkdownTOC -->


### Comments I

| name | posts  | comments   |
|------|--------|------------|
| u1     | page1  | 90       |
| u1     | page2  | 50       |
| u1     | page3  | 40       |
| u1     | page4  | 35       |
| u2     | page2  | 55       |
| u2     | page4  | 45       |
| u4     | page4  | 30       |
| u4     | page3  | 40       |
| u3     | page2  | 100      |

``` sql
CREATE TABLE comments (
    name            varchar(80),
    posts           varchar(80),
    comments         int
);

INSERT INTO comments VALUES ('u1', 'page1', '90');
INSERT INTO comments VALUES ('u1', 'page2', '50');
INSERT INTO comments VALUES ('u1', 'page3', '40');
INSERT INTO comments VALUES ('u1', 'page4', '35');
INSERT INTO comments VALUES ('u2', 'page2', '55');
INSERT INTO comments VALUES ('u2', 'page4', '45');
INSERT INTO comments VALUES ('u4', 'page4', '30');
INSERT INTO comments VALUES ('u4', 'page3', '40');
INSERT INTO comments VALUES ('u3', 'page2', '100');

```

#### Calculate the average comments for the users with >= 2 posts, and `each` post has comments greater or equal to 40

``` sql
-- solution
SELECT 
      name,
      COUNT(DISTINCT posts) as no_of_posts
FROM comments a
  -- This is to ensure that every user selected has comments >= 40 on each post(Nested sub-query)
  WHERE 40 <= ALL(SELECT comments FROM comments WHERE name = a.name) 
GROUP BY name
-- use HAVING when putting conditions on Aggregate Functions
HAVING COUNT(DISTINCT posts) >= 2;  
```

### Article Views

table name: article_views

| date | viewer_id | article_id | author_id | 
|----|----|----|----|                   
|2017-08-01|  123 | 456| 789|                
|2017-08-02|  432 | 543| 654|
|2017-08-01|  789 | 456| 789|
|2017-08-03|  567 | 780| 432|
|2017-08-03|  567 | 780| 432|
|2017-08-01|  789 | 457| 789|


``` sql
CREATE TABLE article_views (
    date            timestamp,
    viewer_id       int,
    article_id      int,
    author_id       int
);
 
INSERT INTO article_views VALUES ('2017-08-01',123,456,789);
INSERT INTO article_views VALUES ('2017-08-02',432, 543,654);
INSERT INTO article_views VALUES ('2017-08-01',789,456,789);
INSERT INTO article_views VALUES ('2017-08-03',567,780,432);
INSERT INTO article_views VALUES ('2017-08-01',789,457,789);
```

#### How many article authors have never viewed their own article? 

``` sql

-- solution
SELECT
	article_id,
  author_id
FROM article_views av1
	WHERE author_id NOT IN (SELECT viewer_id FROM article_views av2 WHERE av2.article_id = av1.article_id);
```

#### How many members viewed more than one articles on 2017-08-01

``` sql
-- solution
SELECT
	viewer_id,
	COUNT(DISTINCT article_id)
FROM article_views
	WHERE DATE(date) = '2017-08-01'
GROUP BY viewer_id
HAVING COUNT(DISTINCT article_id) > 1
```


