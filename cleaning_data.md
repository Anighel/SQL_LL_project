What issues will you address by cleaning the data?

1) Remove leading spaces in Sales_Report, change types for the columns
2) Transforming SKU to just 7 numbers with leading zeros(abandoned but 
   wanted to show my work still)
3) Changing the City and County column to provide nulls if there was not a real city
4) Casting the product price into the price per unit and update the column
5) Changing v2productcategory to return a single word(the word after Home/)
   Accomplished in 2 queries


Queries:
Below, provide the SQL queries you used to clean your data.

1)
ALTER TABLE sales_report
ALTER COLUMN NAME TYPE VARCHAR USING (trim(NAME)),
ALTER COLUMN STOCKLEVEL TYPE int USING (trim(stocklevel)::integer),
ALTER COLUMN restockingleadtime TYPE int USING (trim(restockingleadtime)::integer),
ALTER COLUMN sentimentmagnitude TYPE float USING (trim(sentimentmagnitude)::float(5)),
ALTER COLUMN sentimentscore TYPE float USING (trim(sentimentscore)::float(5)),
ALTER COLUMN ratio TYPE float USING (trim(ratio)::float(5))

2) 
SELECT LPAD(REGEXP_REPLACE(sbs.sku, '\D', '', 'g'), 7, '0'),
sr.sku
FROM sales_by_sku as sbs
join sales_report as sr
on sbs.sku = sr.sku

3)
update all_sessions
set city = case 
	WHEN city = 'not available in demo dataset' then NULL
	when city = '(not set)' then null
	 else city end

update all_sessions
set country = case 
	when country = '(not set)' then null
	 else country end
4)
update all_sessions
set productprice = CAST(productprice AS float) / 1000000
from all_sessions

5)
UPDATE all_sessions
SET v2productcategory = replace(v2productcategory,'Home/', '')
 from all_sessions;

update all_sessions
set v2productcategory =
case 
	when v2productcategory like '(not set)'
	then NULL
	else
REGEXP_REPLACE(v2productcategory, '\/.*$', '') 
end 
from all_sessions

