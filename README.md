# dataanalyst_interview_cramming_package

SQL Tips:  
Checklist in the Tech Interveiw
Understand the tables. Speak about your understanding with you intreviewer to confirm
Write down the table you need
Start with small
Specify table in select
Alias
Rename column
Order 

Database query
Update set
Delete from
CREATE TABLE customers(id int, FirstName varchar(255));
INSERT INTO customers(FirstName, LastName, address, email)
VALUES ('Jason', 'Dsouza', 'McLaren Vale, South Australia', 'test@fakeGmail.com');
Alter table my table
Add default
Drop 

NULL: 
SELECT NULL/0
SELECT NULL+1
SELECT NULL+'1'
Error:
SELECT AVG (NULL)
SELECT MAX (NULL)
SELECT SUM (NULL)
SELECT 0/0
 
Tricky questions
SELECT Max ('TD')  -TD
SELECT MAX  (1,3,8) - Error
SELECT Max ('TD'+'AD')  - TDAD
select * from 'Employee'  - Syntax error
2 <> NULL  -Null
3 NOT IN (1, 2, NULL)  - False

Data types/Special select
CAST(ranks as signed)
COALESCE(NULL, NULL, NULL, 'W3Schools.com');
NVL()
 
 
DATE Function
DATE_ADD('1998-01-02', INTERVAL 31 DAY)  
DATE_SUB("2017-06-15", INTERVAL 10 DAY)
EXTRACT(YEAR FROM '1999-07-02') 
DATE_TRUNC('month'  , cleaned_date)
DATENAME(weekday, '2017/08/25')
extract(year_month from program_date)="202006")
DATEPART(year, '2017/08/25')
DATEDIFF(year, '2017/08/25', '2011/08/25') 
CURRENT_DATE()
 
Numeric
CEILING: Upward
FLOOR: Downward
TRUNCATE(345.156, -2)
ISNUMERIC(4567)
 
String
POSITION('A' IN descript)
SUBSTR(date, 4, 2)
group_concat
 
Windows
NTILE(4) OVER (PARTITION BY start_terminal ORDER BY duration_seconds)
LAG(duration_seconds, 1) OVER(PARTITION BY start_terminal ORDER BY duration_seconds)
 
Get index 1-10
with recursive cte as 
(select 1 as ids
    union all
    select ids+1 from cte
    where ids<10)
select ids
from cte 
 
Moving average
select *,
  avg(Price) OVER(ORDER BY Date
     ROWS BETWEEN 2 PRECEDING AND CURRENT ROW )
     as moving_average
from stock_price;
 
 
 
User Cohort Analysis
Find the first_login of each user
Left join by user_id and datediff=1
Group by first_day and count user_id
 
User continuously use
Get Row_number order by date
Group by date-ranks and select max, min date
Results: user_id, startdate, enddate (continusly visit)
 
Continous seats
select distinct c.seat_id
from cinema c
join cinema c1
on abs(c1.seat_id-c.seat_id)=1
and c.free=1 and c1.free=1
order by 1
 
Common Friends:
WITH temp AS (
  SELECT
    user1_id AS user_id,
    user2_id AS friend_id
  FROM
    Friendship
  UNION
  SELECT
    user2_id AS user_id,
    user1_id AS friend_id
  FROM
    Friendship)
 
SELECT
  a.user1_id,
  a.user2_id,
  COUNT(*) AS common_friend
FROM
  Friendship a
  JOIN temp f1 
  ON a.user1_id = f1.user_id AND a.user2_id != f1.friend_id
  JOIN temp f2 
  ON a.user2_id = f2.user_id AND a.user1_id != f2.friend_id
WHERE
  a.user1_id < a.user2_id
  AND f1.friend_id = f2.friend_id
GROUP BY 1,2
HAVING COUNT(*) >= 3;
