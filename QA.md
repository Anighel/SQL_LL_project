What are your risk areas? Identify and describe them.

This database really needs to be thrown into the ETL process a few times.

Product name -- through my analysis i noticed that there was some words inth
the product names such as "google" or "youtube"


QA Process:
Describe your QA process and include the SQL queries used to execute it.

1) Product name:  started with just a simple distinct query to find the names that
		dont belong.  Solution would be to make a case statement to clean
		it with a replace() statement.


select distinct v2productname
from all_sessions
where v2productname like
-- 'Android%' 
-- 'Google%' 
-- 'Waze%'
-- 'YouTube%'

2) City Data: There is a 8656 out of 15134 NULLS for City data.  This really skews a lot of
the questions that were asked in this exercise. 

select city from 
all_Sessions
where city is null

3) Product Category.  Column should not be nullable. I also may have created nulls with tampering 
with original data.  I may need a better solution as Shop by Brand Category is also not a great
category.

Unfortunatly this was one that i could not solve in time to make a proper query but will show you my 
attempts. 

-->>>> My attempts to split up categories using the delimiter '/' - was unsuccessfull
-- SELECT SUBSTR(v2productcategory, 6, 10) AS ExtractString
-- from all_sessions


-- SELECT RIGHT(v2productcategory , POSITION (5) REVERSE(v2productcategory))-1)
-- FROM ALL_SESSIONS

-- select regexp_replace(v2productcategory, E'HOME/', '')
-- FROM ALL_SESSIONS

-- select SUBSTRING(v2productcategory FROM (LOCATE('HOME/',v2productcategory)+1)) from ALL_SESSIONS

-- SELECT
--   CASE
--     WHEN v2productcategory LIKE '%HOME%/' THEN ''
--   END AS middle_word
-- FROM ALL_SESSIONS
