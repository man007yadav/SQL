`Manoj Yadav` | `SQL Problems Collection`

<!-- MarkdownTOC -->

- [Comments I](#comments-i)
  - [Calculate the average comments for the users with >= 2 posts, and `each` post has comments greater or equal to 40](#calculate-the-average-comments-for-the-users-with--2-posts-and-each-post-has-comments-greater-or-equal-to-40)
- [Article Views](#article-views)
  - [How many article authors have never viewed their own article?](#how-many-article-authors-have-never-viewed-their-own-article)
  - [How many members viewed more than one articles on 2017-08-01](#how-many-members-viewed-more-than-one-articles-on-2017-08-01)
- [Companies](#companies)
  - [count members who ever moved from Microsoft to Google](#count-members-who-ever-moved-from-microsoft-to-google)
  - [count members who directly moved from Microsoft to Google? \(Microsoft -- Linkedin -- Google doesn't count\)](#count-members-who-directly-moved-from-microsoft-to-google-microsoft----linkedin----google-doesnt-count)
- [Continents](#continents)
  - [find the country with largest population in each continent, with strictly output: continent, country, population.](#find-the-country-with-largest-population-in-each-continent-with-strictly-output-continent-country-population)
  - [now for each continent, find the country with largest % of population in given continent. write SQL, then write Python.](#now-for-each-continent-find-the-country-with-largest-%-of-population-in-given-continent-write-sql-then-write-python)
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

### Companies

table
member_id, company_name, year_start

``` sql
CREATE TABLE companies (
    member_id            int,
    company_name       varchar(80),
    year_start      int
);

INSERT INTO companies VALUES (1,'Google', 1990);
INSERT INTO companies VALUES (1,'Microsoft', 2000);
INSERT INTO companies VALUES (2,'Microsoft', 2000);
INSERT INTO companies VALUES (2,'Google', 2001);
INSERT INTO companies VALUES (3,'Microsoft', 1997);
INSERT INTO companies VALUES (3,'Google', 1998);
INSERT INTO companies VALUES (4,'Microsoft', 1997);
INSERT INTO companies VALUES (4,'LinkedIn', 1998);
INSERT INTO companies VALUES (4,'Google', 2000);
```

#### count members who ever moved from Microsoft to Google

``` sql
SELECT
    a.member_id,
    a.company_name,
    a.year_start,
    b.company_name,
    b.year_start
FROM companies a, companies b
	WHERE a.member_id = b.member_id
	AND a.company_name = 'Microsoft'
	AND b.company_name = 'Google'
	AND a.year_start < b.year_start;
```

#### count members who directly moved from Microsoft to Google? (Microsoft -- Linkedin -- Google doesn't count)

```sql
SELECT
    a.member_id,
    a.company_name,
    a.year_start,
    b.company_name,
    b.year_start
FROM companies a, companies b
	WHERE a.member_id = b.member_id
	AND a.company_name = 'Microsoft'
	AND b.company_name = 'Google'
	AND a.year_start < b.year_start
	AND a.member_id NOT IN ( SELECT a.member_id
				FROM companies a, companies b, companies c
				WHERE a.member_id = b.member_id
                                AND a.member_id = c.member_id
                                -- Making sure there is an intermediate company between a and b
                                AND a.year_start < c.year_start
                                AND c.year_start < b.year_start
                                AND a.company_name = 'Microsoft'
                                AND b.company_name = 'Google');

```

### Continents

a table with: continent, country, population

``` sql
CREATE TABLE continents (
    continent          varchar(80),
    country            varchar(80),
    population         int
);

INSERT INTO continents VALUES ('Asia','China', 100);
INSERT INTO continents VALUES ('Asia','India', 100);
INSERT INTO continents VALUES ('Africa','South Africa', 50);
INSERT INTO continents VALUES ('Africa','Egypt', 20);
INSERT INTO continents VALUES ('North America','USA', 50);
INSERT INTO continents VALUES ('North America','Canada', 50);
```

#### find the country with largest population in each continent, with strictly output: continent, country, population. 

Consider corner case that two country have same largest population in the same continent

```sql
-- solution 1
SELECT 
	a.country,
    	a.continent,
    	a.population
FROM continents a 
	INNER JOIN (SELECT
			country,
		    -- RANK() gives same rank to clashing values and counts rest after their sum like 1,1,3..
		    RANK() OVER(PARTITION BY continent ORDER BY population DESC) AS population_rank
			FROM continents) b
		    ON a.country = b.country
			WHERE population_rank = 1;

-- solution 2
SELECT
	a.continent,
    	a.country,
    	a.population
FROM continents a
	INNER JOIN (SELECT
			continent,
			MAX(population) AS max_population
			FROM continents
			GROUP BY continent) b
	ON a.continent = b.continent
    	AND a.population = b.max_population;
```

Note:

    Window functions are permitted only in the SELECT list and the ORDER BY clause of the query. They are forbidden elsewhere, such as in GROUP BY, HAVING and WHERE clauses. This is because they logically execute after the processing of those clauses. Also, window functions execute after regular aggregate functions. This means it is valid to include an aggregate function call in the arguments of a window function, but not vice versa.






