Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
select 
als.country,
sum(cast(a.units_sold as float) * cast(a.unit_price as float)) as Total
from analytics as a
join all_sessions as als
on a.fullvisitorid = als.fullvisitorid
where units_sold is not null
group by als.country
order by Total desc;

select 
als.city,
sum(cast(a.units_sold as float) * cast(a.unit_price as float)) as Total
from analytics as a
join all_sessions as als
on a.fullvisitorid = als.fullvisitorid
where units_sold is not null
group by als.city
order by Total desc


Answer: Top Country was United States, Top City was Mountain View




**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

select round(avg(cast(productquantity as numeric)),2) as Country_AVG, country
from all_sessions
where productquantity is not null
group by country

Answer: spain with 10, us with 4.02 and all others 1

select round(avg(cast(productquantity as integer)),2) as CITY_avg, city
from all_sessions
where productquantity is not null
group by city
order by city_avg desc


Answer: Top 2 were Madrid and Salem





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

select  als.v2productcategory,
		als.country, sum(cast(ana.units_sold as integer))
from all_sessions as als
join analytics as ana 
on als.fullvisitorid = ana.fullvisitorid
where units_sold is not null
group by als.v2productcategory, als.country
order by country

select  als.v2productcategory,
		als.city, sum(cast(ana.units_sold as integer))
from all_sessions as als
join analytics as ana 
on als.fullvisitorid = ana.fullvisitorid
where units_sold is not null
group by als.v2productcategory, als.city
order by city

Answer:

United States orders the bulk the items
Chechia Seems to only order the same time of thing(which is unknown as there is no category data)
Hong Kong mostly ordres electronics
Denmark has only bought 1 thing, 
Charlotte orders a lot of bags
Mountain view has bought over 6k in accesories
There is too much city data missing to really be accurate




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

select 
country,
als.v2productname,
sum(cast(a.units_sold as float)*cast(a.unit_price as float))as Total

from all_sessions as als
join analytics as a USING (visitid)
where a.units_sold is not null
group by  country, als.v2productname
order by Total desc



Answer: i could not reliably find a great quesry for this.  I spent 4 hours with it
trying to use CTE's and the best i got was 132 rows instead of the 30 there should of 
been.  





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

With Top_units as(
select 
country,
als.v2productname,
sum(cast(a.units_sold as float)*cast(a.unit_price as float))as Total

from all_sessions as als
join analytics as a USING (visitid)
where a.units_sold is not null
group by  country, als.v2productname
order by Total desc;

with Revenue as(
select 
als.city,
sum(cast(a.units_sold as float)*cast(a.unit_price as float))as Total
from all_sessions as als
join analytics as a USING (visitid)
group by city	)
Select 
	city,
	Total
From Revenue
where Total is not null
order by total desc


Answer: The majority of come from north america, with United States making 98% of our total worldwide sales
and from the cities New york, Sunnyvale and Mountainview. We should focus on these areas to increase sales!







