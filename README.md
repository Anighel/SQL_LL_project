# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
I was really looking forward to sinking my teeth into a large database to see how it reacted to my Queries.   
Addding tables and importing data from csv is also something i wanted to get practice in to use for my Wife's
Business.

Lastly i really wanted to try everything we had learned sofar in my queries so that i could get better at them, 
even if the queries failed to give be the best desired result(or failed altogether).
## Process
### STEP 1: I spent 2 days just looking at the data, joining some tables to see functionality and wrote down areas that 
            i thought needed cleaning.  I also started thinking of what columns would make good primary keys, what 
	    type they should be and if NULLS were permitted.	I decided to make the type of most columns VARCHAR just
	    so that i could get a hang of the cast function. I cleaned what data i felt i had time to and moved onto analytics.

### STEP 2:  The bulk of my time was spent answering the questions, which i tried many different ways to do so until i was
	     satisfied with the outcome.  Along the way, i found more data to clean which really made me realise i should of 
	     perhaps spent another day cleaning.  Answering the questions took a long time, however coming up with others
	     did not take as much time.  

## Results
I found more ways on what the data COULDN'T tell me more than what it could.  There was too much missing data on some things and
i heavily relied on the all_sessions and analytics tables.  I barely used the sales_report table as if felt like was missing 
columns.  It seems like all_sessions was the most abundant but hardest to work with table.

## Challenges 
The biggest challenge i had was the data cleaning.  I could have taken the whole project time and just cleaned data.  This made
me make some choices that were actually wrong when it came to cleaning.  I spent a whole half a day changing the skus to 
numeric when there was no reason as i had used the wrong tables to compare uniqueness.  It effected my analytics as i did not have
as much time or would have to do some more cleaning in the middle of my analytics.

## Future Goals
I would take the time to remove erronious columns, and add ones that make sence like unit price in products.  Clean up the data more 
and make it easier to join.
