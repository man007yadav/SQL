`Manoj Yadav` | `SQL Problems Collection`

<!-- MarkdownTOC -->

- [Comments I](#comments-i)
  - [Calculate the average comments for the users with >= 2 posts, and `each` post has comments greater or equal to 40](#calculate-the-average-comments-for-the-users-with--2-posts-and-each-post-has-comments-greater-or-equal-to-40)
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
HAVING COUNT(DISTINCT posts) >= 2  
```
