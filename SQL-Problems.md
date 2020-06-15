`Manoj Yadav` | `SQL Problems Collection`

<!-- MarkdownTOC -->

- [Comments I](#comments-i)
  - [Calculate the average comments for the users with >= 2 posts, and `each` post has comments greater or equal to 40](#calculate-the-average-comments-for-the-users-with--2-posts-and-each-post-has-comments-greater-or-equal-to-40)
- [Comments II](#comments-ii)
  - [What is the distribution of comments?](#what-is-the-distribution-of-comments)
  - [Now what if content_type becomes {comment, video, photo, article}，what is the comment distribution for each content type?](#now-what-if-contenttype-becomes-comment-video-photo-article，what-is-the-comment-distribution-for-each-content-type)
- [Messages](#messages)
  - [What can we get some insights from this table?](#what-can-we-get-some-insights-from-this-table)
  - [Write a query about the distribution of number of conversations among users on someday. Before we run any SQL, what is your gut sense that what the distribution will look like? Why?](#write-a-query-about-the-distribution-of-number-of-conversations-among-users-on-someday-before-we-run-any-sql-what-is-your-gut-sense-that-what-the-distribution-will-look-like-why)
  - [Write a query that we can find the top partner who sends the most number of messages to each user. And then add a outer query to calculate the following ratio:](#write-a-query-that-we-can-find-the-top-partner-who-sends-the-most-number-of-messages-to-each-user-and-then-add-a-outer-query-to-calculate-the-following-ratio)
- [Friends](#friends)
  - [Calculate the overall friend accept rate within a time range.](#calculate-the-overall-friend-accept-rate-within-a-time-range)
  - [Who has most friends?](#who-has-most-friends)
- [Friend II](#friend-ii)
  - [Generate friend request acceptance rate](#generate-friend-request-acceptance-rate)
  - [Generate the friend request acceptance rate for people who accept within 24 hours.](#generate-the-friend-request-acceptance-rate-for-people-who-accept-within-24-hours)
- [CTR](#ctr)
- [CTR II](#ctr-ii)
  - [Assuming ctr is defined as total number clicks / total number of impressions \(not counting each unique user’s action\)](#assuming-ctr-is-defined-as-total-number-clicks--total-number-of-impressions-not-counting-each-unique-user’s-action)
- [User Status](#user-status)
  - [Assume two tables, Tracking {user, state} and Day {user}](#assume-two-tables-tracking-user-state-and-day-user)
- [Notifications](#notifications)
  - [How many users turned feature on till now?](#how-many-users-turned-feature-on-till-now)
  - [How many users have ever turned the feature on?](#how-many-users-have-ever-turned-the-feature-on)
  - [In a table that tracks the status of every user every day, how would you add today’s data to it?](#in-a-table-that-tracks-the-status-of-every-user-every-day-how-would-you-add-today’s-data-to-it)
- [Recommendations](#recommendations)
  - [Write a SQL that makes recommendations using the pages that your friends liked. It should not recommend pages you already liked.](#write-a-sql-that-makes-recommendations-using-the-pages-that-your-friends-liked-it-should-not-recommend-pages-you-already-liked)
- [Phone Logins](#phone-logins)
  - [How many login_confirmation was sent by different carrier in different country yesterday?](#how-many-loginconfirmation-was-sent-by-different-carrier-in-different-country-yesterday)
  - [How to analyze why the number of logins dropped.](#how-to-analyze-why-the-number-of-logins-dropped)
- [Article Views](#article-views)
  - [How many article authors have never viewed their own article?](#how-many-article-authors-have-never-viewed-their-own-article)
  - [How many members viewed more than one articles on 2017-08-01](#how-many-members-viewed-more-than-one-articles-on-2017-08-01)
- [Companies](#companies)
  - [count members who ever moved from Microsoft to Google](#count-members-who-ever-moved-from-microsoft-to-google)
  - [count members who directly moved from Microsoft to Google? \(Microsoft -- Linkedin -- Google doesn't count\)](#count-members-who-directly-moved-from-microsoft-to-google-microsoft----linkedin----google-doesnt-count)
- [Continents](#continents)
  - [find the country with largest population in each continent, with strictly output: continent, country, population.](#find-the-country-with-largest-population-in-each-continent-with-strictly-output-continent-country-population)
  - [now for each continent, find the country with largest % of population in given continent. write SQL, then write Python.](#now-for-each-continent-find-the-country-with-largest-%-of-population-in-given-continent-write-sql-then-write-python)
- [Projects](#projects)
  - [Find the number of unique employees per project per month?](#find-the-number-of-unique-employees-per-project-per-month)
  - [For each employee, a list of projects he/she works on Write a script/function/else that reads data from CSV file and creates a data structure that stores, for each project, a list of employees who work on it.](#for-each-employee-a-list-of-projects-heshe-works-on-write-a-scriptfunctionelse-that-reads-data-from-csv-file-and-creates-a-data-structure-that-stores-for-each-project-a-list-of-employees-who-work-on-it)
- [Pivot/ Unpivot](#pivot-unpivot)
  - [unpivot](#unpivot)
  - [pivot the table above](#pivot-the-table-above)
- [Ads](#ads)
  - [The fraction of advertiser has at least 1 conversion?](#the-fraction-of-advertiser-has-at-least-1-conversion)
  - [What metrics would you show to advertisers \(ROI\)?](#what-metrics-would-you-show-to-advertisers-roi)
- [Student](#student)
  - [What was the overall attendance rate for the school district yesterday?](#what-was-the-overall-attendance-rate-for-the-school-district-yesterday)
  - [Which grade level currently has the most students in this school district?](#which-grade-level-currently-has-the-most-students-in-this-school-district)

<!-- /MarkdownTOC -->


### Comments I

| name | posts  | comments   |
|------|--------|------------|
| u1     | page1  | 90       |
| u1     | page2  | 50       |
| u1     | page3  | 40       |
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
INSERT INTO comments VALUES ('u2', 'page2', '55');
INSERT INTO comments VALUES ('u2', 'page4', '45');
INSERT INTO comments VALUES ('u4', 'page4', '30');
INSERT INTO comments VALUES ('u4', 'page3', '40');
INSERT INTO comments VALUES ('u3', 'page2', '100');

-- or you can do 

copy comments from '/Users/jennifer/dev/sql_data_exercise/comments.csv' CSV HEADER
```

#### Calculate the average comments for the users with >= 2 posts, and `each` post has comments greater or equal to 40

``` sql
-- solution
select a.name, round(avg(a.comments),2) from comments a
inner join

-- get users who has more than two posts and each posts with more than 40 comments
(select name from comments
where comments >= 40
group by name
having count(distinct posts) >= 2) b

on a.name = b.name
group by a.name;
```

### Comments II

table: content_id | content_type (comment/ post) | target_id

If it is comment，target_id is the userid who posts it.

If it is post, then target_id is NULL.



#### What is the distribution of comments?


``` sql
select cnt, count(cnt) as freq
from
    (select content_id, count(target_id) cnt 
    from table 
     where content_type = 'comment'
    group by content_id) a 
group by cnt;
```

#### Now what if content_type becomes {comment, video, photo, article}，what is the comment distribution for each content type?

``` sql

select content_type, cnt, count(cnt) as freq
from (
    select a.content_id, a.content_type, count(b.target_id) cnt
    from table a
    group by a.content_id, a.content_type) tmp
group by content_type
order by content_type, cnt;

```

### Messages

table: date | u1 | u2 | n_msg

n_msg: the number of messsages between one unique user pair at someday.


#### What can we get some insights from this table?

user activities, represent closeness.

#### Write a query about the distribution of number of conversations among users on someday. Before we run any SQL, what is your gut sense that what the distribution will look like? Why?

``` sql
select conversations, count(u1) freq
from
(select u1, count(distinct u2) conversations from table1
where n_msg > 0 and date = SOMEDAY
group by u1) a
group by conversations
order by conversations
```

very skew data on left tail

#### Write a query that we can find the top partner who sends the most number of messages to each user. And then add a outer query to calculate the following ratio:

sum(n_msg_with_top_partners) / sum(n_msg_with_all_contacts)


```
select cast(sum(sum_top) as float)/(select sum(n_msg) from table) as fraction

from (
-- top partners
select u1, max(sum_n_msg) sum_top from 
(select u1, u2, sum(n_msg) sum_n_msg from table1
group by u1, u2) tmp
group by u1
) tmp2

```

### Friends

table friending: action_id, target_id, action（accept, request, unfriend), date, time

#### Calculate the overall friend accept rate within a time range.

``` sql

select sum(accept)/cast(sum(request) as float) from

-- accept

(select a.action_id, count(a.target_id) accept from table1 a, table2 b
where a.target_id = b.action_id
      and a.action ='accept'
      and b.action ='request'
) a,
-- request

(select action_id, count(target_id) request from table1
where action = 'request') b;
```

#### Who has most friends?

``` sql
select user_id, sum(cnt) as n_friend
from (
    (select action_id as user_id,
            sum(case when accept = 'accept' then 1
            when accept = 'unfriend' then -1
            else 0 end) as cnt
    from table)
    union all
    (select target_id as user_id, 
            sum(case when accept = 'accept' then 1
            when accept = 'unfriend' then -1
            else 0 end) as cnt
    from table)
) a
group by user_id
order by n_friend desc
limit 1
```

### Friend II

Table: friending (date | time | action | actor_id | target_id)

action = {‘send_request’,‘accept_request’}

#### Generate friend request acceptance rate

``` sql

select cast(sum(accept) as float)/sum(request) from
-- accept
(
select a.actor_id, count(distinct b.target_id) accept from table1 a, table1 b
where a.target_id = b.actor_id
     and a.action = 'accept_request'
     and b.action = 'send_request'
group by a.actor_id) a,

-- request 
(
select actor_id, count(distinct target_id) request from table1
where action = 'send_request'
group by actor_id) b;
```

#### Generate the friend request acceptance rate for people who accept within 24 hours.

``` sql
select cast(sum(accept) as float)/sum(request) from
-- accept
(
select a.date, a.actor_id, count(distinct b.target_id) accept from table1 a, table1 b
where a.target_id = b.actor_id
     and a.action = 'accept_request'
     and b.action = 'send_request'
     and datepart('day', a.date-b.date) <= 1
group by a.date, a.actor_id) a,

-- request 
(
select date, actor_id, count(distinct target_id) request from table1
where action = 'send_request'
group by date, actor_id) b

where datepart('day', a.date-b.date) <= 1;
```

### CTR

table1: time, user_id, app, event（impression，click, null).

If the user saw it and clicked it, then the event is click. If the user saw it but did not click, then the event is impression. The event is null, which means the user did not see it.

 #### Get the click through rate.
 
 ``` sql
 select a.app, COALESCE(b.clicks,0)/cast(a.impression,float) from
 -- impression
 (select app, count(user_id) impression
 from table1
 where event is not null
 group by app) a,
 -- clicks
 left join
 (select app, count(user_id) clicks
 from table1
 where event = 'click'
 group by app) b
 
 on a.app = b.app
 
 ```
 
 #### What if CTR is over 100%? Please justify any reason that could cause this problem.
 
 For each impression, we might have more than one click. So we need choose the right metric to represent the click through rate.

Here we want to clarify the difference between CTR (click through rate) and CTP (click through probability).

When calculating we need to make sure click is from the users who viewed it.
 
 ``` sql
select a.app, COALESCE(a.clicks,0)/cast(b.impression as float) from
-- clicks
(select a.app, count(distinct a.user_id) clicks from table1 a
inner join table1 b
on a.app = b.app and a.user_id = b.user_id
where a.event = 'click' and b.event = 'impression'
group by a.app) a

left join
 -- impression
 (select app, count(user_id) impression
 from table1
 where event is not null
 group by app) b

on a.app = b.app
 ```

### CTR II

#### Assuming ctr is defined as total number clicks / total number of impressions (not counting each unique user’s action)

``` sql
select
    appid,
    total_click_ct / total_imp_ct as ctr
from (
    select
        appid,
        count(distinct case when flag = 'imp' then 1 else 0 end) as total_imp_ct,
        count(distinct case when flag = 'click' then 1 else 0 end) as total_click_ct,
    from table
    where ts > x and ts < y
    group by appid) table2
order by ctr desc;

```

### User Status

Given a table that each day shows who was active in the system and a table that tracks ongoing user status, write a procedure that will take each day’s active table and pass it into the ongoing daily tracking table.

Possible states are:

user stayed (yesterday yes, today yes)

user churned (yesterday yes, today no)

user revived (yesterday no, today yes)

user new (yesterday null, today yes)

Note: you’ll want to spot and account for the undefined state.

#### Assume two tables, Tracking {user, state} and Day {user}

check churn | new | stayed | revived

``` sql
with tmp as (
select case when Tracking.user is not null then Tracking.user else Day.user end as user,
       case when Day.user is null then "churned"
            when Tracking.state is null then "new"
            when Tracking.state <> "churned" then "stayed"
            when Tracking.state = "churned" then "revived"
            else "check" end as state
from Tracking 
full outer join Day
on Tracking.user = Day.user);
```

### Notifications

There is a table that tracks every time a user turns a feature on or off, with columns user_id, action (“on” or “off), date, and time.

user_id | action | date | time

#### How many users turned feature on till now?

``` sql
select count(distinct user_id) from 
(select user_id, sum(case when action is 'on' then 1
                     when action is 'off' then -1
                     else 0 end as status)
from table1
group by user_id) tmp
where status > 0;

```

#### How many users have ever turned the feature on?

``` sql
select count(distinct user_id) from table1
where action = 'on';
```

#### In a table that tracks the status of every user every day, how would you add today’s data to it?

- historical_data: user_id, action (unique pair)

- today: user_id, action

```
with tmp as (
select user_id,
case when on_cnt - off_cnt = 1 then 'on' else 'off' end as action
from 
    (select user_id, 
    sum(case when action='on' then 1 else 0) on_cnt,
    sum(case when action='off' then 1 else 0) off_cnt
    from 
        (select user_id, action from historical_data
        union all
        select user_id, action from today) a
    group by user_id) b);
```

### Recommendations

two tables

friends_table: user_id | friend_id

pages_table: user_id | post_id

#### Write a SQL that makes recommendations using the pages that your friends liked. It should not recommend pages you already liked.

``` sql
select 
    a.user_id, 
    b.post_id
from friends_table a
join pages_table b
on a.friends_id = b.user_id
where (a.user_id, b.post_id) not in (select user_id, post_id from pages_table)
order by a.user_id, b.post_id
```

### Phone Logins

attempts: date | country | carrier | phone_no | type (‘login_confirmation’| ‘notification’)

logins: date | phone_no


#### How many login_confirmation was sent by different carrier in different country yesterday?

``` sql
select country, carrier, count(phone_no)
from attempts
where type = 'login_confirmation'
      and datepart('day', now() - date) <= 1
group by country, carrier;
```

#### How to analyze why the number of logins dropped. 

plot it and see how carrier perform in each country by date

``` sql
select 
    x.date, 
    x.country, 
    x.carrier, 
    round(y.total_logins/x.total_attempts, 2) as login_rate
from
    (select date, country, carrier, count(distinct phone_no) total_attempts 
    from attempts
    where type = 'login_confirmation'
    group by date, country, carrier
    ) x
join
    (select a.date, a.country, a.carrier, count(distinct a.phone_no) total_logins 
    from attempts a
    join logins b
    on a.date = b.date and a.phone_no = b.phone_no
    where a.type = 'login_confirmation'
    group by a.date, a.country, a.carrier
    ) y
on x.date=y.date 
and x.country=y.country 
and x.carrier=y.carrier
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
|2017-08-01|789|457   |789


``` sql
CREATE TABLE article_views (
    date            timestamp,
    viewer_id       int,
    article_id      int,
    author_id       int
);
 
INSERT INTO article_views VALUES ('2017-08-01',123,	456	,789);
INSERT INTO article_views VALUES ('2017-08-02',432	,543,	654);
INSERT INTO article_views VALUES ('2017-08-01',789,	456	,789);
INSERT INTO article_views VALUES ('2017-08-03',567,	780,	432);
INSERT INTO article_views VALUES ('2017-08-01',789, 457    ,789);
```

#### How many article authors have never viewed their own article? 

``` sql

-- solution
select count(distinct a.author_id) from article_views a
where a.author_id not in 
(select a.author_id from article_views a
where a.author_id = a.viewer_id);
```

#### How many members viewed more than one articles on 2017-08-01

``` sql
-- solution
select viewer_id from article_views
where date = TIMESTAMP '2017-08-01'
group by viewer_id
having count(article_id) > 1;
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

select count(distinct a.member_id) from companies a, companies b
where a.member_id = b.member_id
      and a.year_start < b.year_start
      and a.company_name = 'Microsoft'
      and b.company_name = 'Google';
```

#### count members who directly moved from Microsoft to Google? (Microsoft -- Linkedin -- Google doesn't count)

``` sql

-- solution 1
select count(distinct a.member_id) from companies a, companies b
where a.member_id = b.member_id
      and a.member_id = b.member_id
      and a.year_start < b.year_start
      and a.company_name = 'Microsoft'
      and b.company_name = 'Google'
      and a.member_id not in
                        (select distinct a.member_id 
                         from companies a, companies b, companies c
                         where a.member_id = b.member_id
                              and a.member_id = b.member_id
                              and a.year_start < b.year_start
                              and c.year_start > a.year_start
                              and c.year_start < b.year_start
                              and a.company_name = 'Microsoft'
                              and b.company_name = 'Google');

-- solution 2
select count(distinct member_id) from (
  select member_id, 
         company_name as current_company_name, 
         year_start, 
         lag(company_name) over (partition by member_id order by          year_start asc) as previous_company_name
  from companies
  ) a
where previous_company_name = 'Microsoft' and current_company_name = 'Google';
```


Note:
    
    lag(value any [, offset integer [, default any ]])	same type as value	returns value evaluated at the row that is offset rows before the current row within the partition; if there is no such row, instead return default. Both offset and default are evaluated with respect to the current row. If omitted, offset defaults to 1 and default to null

### Continents

a table with: continent, country, population

#### find the country with largest population in each continent, with strictly output: continent, country, population. 

Consider corner case that two country have same largest population in the same continent

``` sql
CREATE TABLE continents (
    continent          varchar(80),
    country            varchar(80),
    population         int
);

INSERT INTO continents VALUES ('Asia','China', 100);
INSERT INTO continents VALUES ('Asia','Inida', 100);
INSERT INTO continents VALUES ('Africa','South Africa', 50);
INSERT INTO continents VALUES ('Africa','Egypt', 20);
INSERT INTO continents VALUES ('North America','USA', 50);
INSERT INTO continents VALUES ('North America','Canada', 50);
```

``` sql
-- solution 1
select a.country, b.continent, a.population from continents a
inner join (
    select continent, max(population) max_p from continents
    group by continent
) b
on a.continent = b.continent
and a.population = b.max_p;

-- solution 2

select a.country, a.continent, a.population from continents a
inner join 
(select country, rank() over (partition by continent order by population desc ) as rank
from continents) b
on a.country = b.country
where rank = 1;
```

Note:

    Window functions are permitted only in the SELECT list and the ORDER BY clause of the query. They are forbidden elsewhere, such as in GROUP BY, HAVING and WHERE clauses. This is because they logically execute after the processing of those clauses. Also, window functions execute after regular aggregate functions. This means it is valid to include an aggregate function call in the arguments of a window function, but not vice versa.

#### now for each continent, find the country with largest % of population in given continent. write SQL, then write Python.

``` sql

select a.country, a.continent, round(a.population/c.total*100) ratio_percent from continents a
inner join 
        (select country, rank() over (partition by continent order by population desc ) as rank
        from continents) b
on a.country = b.country
inner join 
        (select continent, CAST(sum(population) as float) total from continents
         group by continent) c
on a.continent = c.continent
where rank = 1 and a.continent = GIVEN_VALUE;

```

### Projects

SQL Given tables:

employees(id, unixname, team, role, days_since_started)

projects(id, name,….)

commits(id, file_path, proj_id, auth_id, timestamp)

#### Find the number of unique employees per project per month?

``` sql
select 
    p.id, 
    extract(month from c.timstamp) as month,
    count(distinct e.id)
from commits c
join employees e
on c.auth_id = e.id
join projects p
on c.proj_id = p.id
group by p.id, month

```

#### For each employee, a list of projects he/she works on Write a script/function/else that reads data from CSV file and creates a data structure that stores, for each project, a list of employees who work on it.

```
john_doe, android, ios, infra 
bob_law, is, backend 
jane_doe, frontend 
..., ..., ...
```
``` python
import collections
projects = collections.defaultdict(list)

with open("test.csv") as df:
    for line in df:
        proj = line.split(",")
        name = proj[0]
        for p in proj[1:]:
            projects[p].append(name)
```

### Pivot/ Unpivot

|date     |qty_prod_a  |qty_prod_b  |qty_prod_c|
|---------|------------|------------|---------|                   
|1/1/2013 |100         |200         |300      |
|1/2/2013 |101         |0           |301      |
|1/3/2013 |102         |202         |302      |

``` sql
CREATE TABLE products (
    date          timestamp,
    qty_prod_a    int,
    qty_prod_b    int,
    qty_prod_c    int
);

INSERT INTO products VALUES ('1/1/2013', 100,200,300);
INSERT INTO products VALUES ('1/2/2013', 101,0,301);
INSERT INTO products VALUES ('1/3/2013', 102,202,302);
```

#### unpivot

- you have a table t1 with the quantity of product A, B, and C sold per day, as shown above
- there are only 3 possible products in the table: A, B, and C
- write SQL code to reformat the data as shown below
- the resulting data should be in 3 columns: {date, product name, quantity sold}

``` sql
select * from (
select date, 'a' as product, qty_prod_a as quantity_sold from products
union 
select date, 'b' as product, qty_prod_b as quantity_sold from products
union
select date, 'c' as product, qty_prod_c as quantity_sold from products
    ) tmp
order by date, product;
```

#### pivot the table above

``` sql
create table products1 as (
select * from (
select date, 'a' as product, qty_prod_a as quantity_sold from products
union 
select date, 'b' as product, qty_prod_b as quantity_sold from products
union
select date, 'c' as product, qty_prod_c as quantity_sold from products
    ) tmp
order by date, product);

SELECT
  date,
  SUM(CASE product WHEN 'a' THEN quantity_sold ELSE 0 END) AS "product.A",
  SUM(CASE product WHEN 'b' THEN quantity_sold ELSE 0 END) AS "product.B",
  SUM(CASE product WHEN 'c' THEN quantity_sold ELSE 0 END) AS "product.C"
FROM products1
GROUP BY date;
```

### Ads

two tables

- adv_info: advertiser_id | ad_id | spend: The Advertiser pay for this ad

- ad_info: ad_id | user_id | price: The user spend through this ad (Assume all prices in this column >0)


``` sql

CREATE TABLE adv_info (
    advertiser_id    int,
    ad_id    int,
    spend    float
);

INSERT INTO adv_info VALUES (10, 200,300);
INSERT INTO adv_info VALUES (11, 100,1000);
INSERT INTO adv_info VALUES (13, 400,3000);
INSERT INTO adv_info VALUES (14, 500,5000);

CREATE TABLE ad_info (
    ad_id    int,
    user_id    int,
    price    float
);

INSERT INTO ad_info VALUES (200, 4,30);
INSERT INTO ad_info VALUES (100, 4,100);
INSERT INTO ad_info VALUES (400, 4,300);
INSERT INTO ad_info VALUES (200, 10,31);
INSERT INTO ad_info VALUES (100, 10,110);
INSERT INTO ad_info VALUES (400, 10,310);
```

#### The fraction of advertiser has at least 1 conversion?

``` sql
select cast(cnt_1 as float)/total conversion_ratio from
(select count(distinct a.advertiser_id) cnt_1  from adv_info a
inner join
    (select ad_id from ad_info) b
on a.ad_id = b.ad_id) tmp1,

(select count(distinct a.advertiser_id) total  from adv_info a) tmp2;
```

#### What metrics would you show to advertisers (ROI)?

``` sql

select a.advertiser_id, a.ad_id, b.revenue/a.spending roi from
(select advertiser_id , ad_id, sum(spend) spending from adv_info
group by advertiser_id, ad_id) a,

(select ad_id, sum(price) revenue from ad_info
group by ad_id) b
where a.ad_id = b.ad_id;

```

### Student

- attendance: date | student_id | attendance

- student: student_id | school_id | grade_level | date_of_birth | hometown

``` sql
CREATE TABLE attendance (
    date    timestamp,
    student_id    int,
    attendance    int -- 0, 1
);

INSERT INTO attendance VALUES ('2018/01/02', 2,1);
INSERT INTO attendance VALUES ('2018/01/02', 1,1);
INSERT INTO attendance VALUES ('2018/01/02', 4,1);
INSERT INTO attendance VALUES ('2018/02/02', 5,1);
INSERT INTO attendance VALUES ('2018/02/22', 1,1);
INSERT INTO attendance VALUES ('2018/02/22', 4,1);
INSERT INTO attendance VALUES ('2018/02/22', 5,1);


CREATE TABLE student (
    student_id    int,
    school_id    int,
    grade_level int,
    date_of_birth timestamp,
    hometown varchar(80)        
);

INSERT INTO student VALUES (1,100, 4 ,'1994/01/02','san francisco');
INSERT INTO student VALUES (2,100, 4 ,'1994/01/02','san francisco');
INSERT INTO student VALUES (3,100, 4 ,'1994/01/02','san francisco');
INSERT INTO student VALUES (4,100, 4 ,'1994/01/02','san francisco');
```

#### What was the overall attendance rate for the school district yesterday?

```
select cast(count(distinct student_id) as float)/(select count(distinct student_id) from student) att_rate from attendance
where date_part('day', now() - date) <= 1
and attendance = 1;
```

#### Which grade level currently has the most students in this school district?
 
 ``` sql
 with tmp as (select grade_level, count(distinct student_id) cnt from student
 group by grade_level
 order by cnt desc)
 
select grade_level from tmp
where cnt = (select max(cnt) from tmp);
 ```

 #### Which school had the average highest attendance rate? the lowest?
 
 ``` sql
 -- take avarage
 -- daily attendance per school
 -- number of students per school
 
 
 select c.school_id, avg(att_rate_per_school_per_day) as avg_rate
from 
    (select a.date, a.school_id, a.att_num/b.total_num as att_rate_per_school_per_day
    from 
        -- date, school, att_num
        (select t1.date, t2.school_id, cast(count(distinct t1.student_id) as float) as att_num 
        from attendance t1
        right join student t2 
        on t1.student_id = t2.student_id 
        where t1.attendance = 1
        group by t1.date, t2.school_id ) a 
    join 
        -- school, total_num
        (select school_id, count(distinct student_id) as total_num
        from student
        group by school_id) b 
    on a.school_id = b.school_id) c 
group by c.school_id 
order by avg_rate desc;
 ```
