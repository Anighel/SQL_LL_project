Question 1: We previously learned that Mountain View was the City that ordered the most from us
What kind of items is Mountain View ordering?

SQL Queries:
select 
als.v2productcategory,
sum(cast(a.units_sold as float) * cast(productprice as float)) as Total
from analytics as a
join all_sessions as als
on a.fullvisitorid = als.fullvisitorid
where city like 'Mountain View'
group by als.v2productcategory
order by Total desc

Answer:  Our top 2 are Nest and Accessories


Question 2:  Do we have enough Nest in stock for, and if not how long to replenish?


SQL Queries: 

select distinct als.productsku,
	   p.name,
	   p.stocklevel,
	   p.restockingleadtime
from all_sessions as als
join products as p 
on als.productsku = p.sku
where v2productcategory like 'Nest' and city like'Mountain View'


select distinct als.productsku,
	   p.name,
	   cast(p.stocklevel as integer) as Stocklevel,
	   p.restockingleadtime
from all_sessions as als
join products as p 
on als.productsku = p.sku
where v2productcategory like 'Nest' and city like'Mountain View'
group by   cast(p.stocklevel as integer) , als.productsku,
	   p.name,  p.restockingleadtime
Having  cast(p.stocklevel as integer) < 100

Answer:
NEST We are out of 2 items with a large restock lead time.  Stock under 100 units shown but moving the having
number to find other answers



Question 3: Find our best selling product by revenue 


SQL Queries: 

select sr.name,
	sum((sr.total_ordered) * cast(als.productprice as float)) AS Grand_Total,
	count(sr.total_ordered) as count
from sales_report as sr
join sales_by_sku sbs USING (sku)
join all_sessions as als
on als.productsku = sr.sku
group by sr.name
order by count--or grand_total
desc


Answer: Our Higest sales are in our security cameras and Nest thermometer, and our top selling item is the Twill capp
