# SQL
Here. I completed tasks related to:

Grouping data using aggregate functions.
Calculating marketing campaign metrics.

### Task 1

Write an SQL query to retrieve the following data from the table facebook_ads_basic_daily:

ad_date - the date the ad was displayed
campaign_id - the unique identifier of the campaign
Aggregated values by date and campaign ID for the following metrics:
total cost
number of impressions
number of clicks
total conversion value

### Task 2

Using the aggregated data on costs and conversions, calculate the following metrics for each date and campaign ID:

CPC
CPM
CTR
ROMI
Group the table by the fields ad_date and campaign_id.

## Solution code
select ad_date
	, campaign_id
	, sum(spend) as "SUM_SPEND"
	, sum(impressions) as "SUM_MPRESSIONS"
	, sum(clicks) as "SUM_CLICKS"
	, sum(value) as "SUM_VALUE"
	, sum(spend)/sum(clicks) as "CPC"
	, (sum(impressions)/SUM(spend))* 1000 as "CPM"
	, round((sum(1.0*clicks)/sum(impressions))*100,1) as "CTR %"
	, ((SUM(value) - SUM(spend))/SUM(spend))*100 as "ROMI"
FROM public.facebook_ads_basic_daily
where true 
	and impressions >0
	and clicks >0
GROUP by ad_date
	, campaign_id
	, spend 
	, clicks
	, impressions 
	, value
