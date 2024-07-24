# [SQL] Ecommerce Dataset Exploring 

## Table of Contents:
1. [Introduction](#clean_data)
2. [Goals](#clean_data)
3. [Import raw data](#cau3)
4. [Read and explain dataset](#cau4)
5. [Exploring the Dataset](#cau5)
6. [Conclusions](#cau6)


## 1. Introduction
- The eCommerce dataset is stored in a public Google BigQuery dataset. This dataset contains information about user sessions on a website collected from Google Analytics in 2017.

- Based on the eCommerce dataset, the author perform queries to analyze website activity in 2017, such as calculating bounce rate, identifying days with the highest revenue, analyzing user behavior on pages, and various other types of analysis. This project aims to have an outlook on the business situation, marketing activity efficiency analyzing the products.

- To query and work with this dataset, the author uses the Google BigQuery tool to write and execute SQL queries.

## 2. Goals
- Overview of website activity
- Bounce rate analysis
- Revenue analysis
- Transactions analysis
- Products analysis

## 3. Import raw data
The eCommerce dataset is stored in a public Google BigQuery dataset. To access the dataset, follow these steps:
- Log in to your Google Cloud Platform account and create a new project.
- Navigate to the BigQuery console and select your newly created project.
- Select "Add Data" in the navigation panel and then "Search a project".
- Enter the project ID **"bigquery-public-data.google_analytics_sample.ga_sessions"** and click "Enter".
- Click on the **"ga_sessions_"** table to open it.
  
## 4. Read and explain dataset
https://support.google.com/analytics/answer/3437719?hl=en
  | Field Name                       | Data Type | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|----------------------------------|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| fullVisitorId                    | STRING    | The unique visitor ID.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| date                             | STRING    | The date of the session in YYYYMMDD format.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| totals                           | RECORD    | This section contains aggregate values across the session.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| totals.bounces                   | INTEGER   | Total bounces (for convenience). For a bounced session, the value is 1, otherwise it is null.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| totals.hits                      | INTEGER   | Total number of hits within the session.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| totals.pageviews                 | INTEGER   | Total number of pageviews within the session.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| totals.visits                    | INTEGER   | The number of sessions (for convenience). This value is 1 for sessions with interaction events. The value is null if there are no interaction events in the session.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| trafficSource.source             | STRING    | The source of the traffic source. Could be the name of the search engine, the referring hostname, or a value of the utm_source URL parameter.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| hits                             | RECORD    | This row and nested fields are populated for any and all types of hits.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| hits.eCommerceAction             | RECORD    | This section contains all of the ecommerce hits that occurred during the session. This is a repeated field and has an entry for each hit that was collected.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| hits.eCommerceAction.action_type | STRING    | The action type. Click through of product lists = 1, Product detail views = 2, Add product(s) to cart = 3, Remove product(s) from cart = 4, Check out = 5, Completed purchase = 6, Refund of purchase = 7, Checkout options = 8, Unknown = 0.Usually this action type applies to all the products in a hit, with the following exception: when hits.product.isImpression = TRUE, the corresponding product is a product impression that is seen while the product action is taking place (i.e., a product in list view).Example query to calculate number of products in list views:SELECTCOUNT(hits.product.v2ProductName)FROM [foo-160803:123456789.ga_sessions_20170101]WHERE hits.product.isImpression == TRUEExample query to calculate number of products in detailed view:SELECTCOUNT(hits.product.v2ProductName),FROM[foo-160803:123456789.ga_sessions_20170101]WHEREhits.ecommerceaction.action_type = 2AND ( BOOLEAN(hits.product.isImpression) IS NULL OR BOOLEAN(hits.product.isImpression) == FALSE ) |
| hits.product                     | RECORD    | This row and nested fields will be populated for each hit that contains Enhanced Ecommerce PRODUCT data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| hits.product.productQuantity     | INTEGER   | The quantity of the product purchased.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| hits.product.productRevenue      | INTEGER   | The revenue of the product, expressed as the value passed to Analytics multiplied by 10^6 (e.g., 2.40 would be given as 2400000).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| hits.product.productSKU          | STRING    | Product SKU.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| hits.product.v2ProductName       | STRING    | Product Name.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| fullVisitorId                    | STRING    | The unique visitor ID.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

## 5. Exploring the Dataset
In this project, I will write 08 queries in Bigquery for this Ecommerce dataset

### Query 01: Calculate total visit, pageview, transaction for January, February and March 2017 (Order by month).
- SQL code
  
~~~~sql
SELECT
  format_date("%Y%m", parse_date("%Y%m%d", date)) as month,
  SUM(totals.visits) AS visits,
  SUM(totals.pageviews) AS pageviews,
  SUM(totals.transactions) AS transactions,
FROM `bigquery-public-data.google_analytics_sample.ga_sessions_2017*`
WHERE _TABLE_SUFFIX BETWEEN '0101' AND '0331'
GROUP BY 1
ORDER BY 1;
~~~~
  
- Query result
  
| Row |  month   |  visits  |  pageviews  |  transactions  | 
|-----|----------|----------|-------------|----------------|
|   1 | 201701   |    64694 |      257708 |            713 |
|   2 | 201702   |    62192 |      233373 |            733 |
|   3 | 201703   |    69931 |      259522 |            993 |

### Query 02: Bounce rate per traffic source in July 2017 (Order by total_visit DESC).
- SQL code
  
~~~~sql
SELECT
    trafficSource.source as source,
    sum(totals.visits) as total_visits,
    sum(totals.Bounces) as total_no_of_bounces,
    ROUND(((sum(totals.Bounces)/sum(totals.visits))* 100),8) as bounce_rate
FROM `bigquery-public-data.google_analytics_sample.ga_sessions_201707*`
GROUP BY source
ORDER BY total_visits DESC;
~~~~
  
- Query result
  
| Row |  source              |  total_visits  |  total_no_of_bounces  |  bounce_rate   |
|-----|----------------------|----------------|-----------------------|----------------|
|   2 | (direct)             |          19891 |                  8606 |     43.2657986 |
|   3 | youtube.com          |           6351 |                  4238 |    66.72964887 |
|   4 | analytics.google.com |           1972 |                  1064 |    53.95537525 |
|   5 | Partners             |           1788 |                   936 |    52.34899329 |
|   6 | m.facebook.com       |            669 |                   430 |    64.27503737 |
|   7 | google.com           |            368 |                   183 |    49.72826087 |
|   8 | dfa                  |            302 |                   124 |    41.05960265 |
|   9 | sites.google.com     |            230 |                    97 |    42.17391304 |
|  10 | facebook.com         |            191 |                   102 |    53.40314136 |

### Query 03: Revenue by traffic source by week, by month in June 2017.
- SQL code
  
~~~~sql
with month_revenue as (
      SELECT
            'Month' as time_type
            ,FORMAT_DATE('%Y%m',PARSE_DATE('%Y%m%d',date)) as time
            ,trafficSource.source
            ,ROUND(SUM(product.productRevenue)/1000000,4) as revenue
      FROM `bigquery-public-data.google_analytics_sample.ga_sessions_201706*`,
      UNNEST (hits) as hits,
      UNNEST (hits.product) as product
      WHERE (_table_suffix between '01' and '31') and product.productRevenue is not null
      GROUP BY source, time, time_type
)

,week_revenue as (
      SELECT
            'Week' as time_type
            ,FORMAT_DATE('%Y%W',PARSE_DATE('%Y%m%d',date)) as time
            ,trafficSource.source
            ,ROUND(SUM(product.productRevenue)/1000000,4) as revenue
      FROM `bigquery-public-data.google_analytics_sample.ga_sessions_201706*`,
      UNNEST (hits) as hits,
      UNNEST (hits.product) as product
      WHERE (_table_suffix between '01' and '31') and product.productRevenue is not null
      GROUP BY source, time, time_type
)

SELECT *
FROM month_revenue
UNION ALL
SELECT *
FROM week_revenue
ORDER BY revenue DESC
~~~~

- Query result

| Row |  source              |  total_visits  |  total_no_of_bounces  |  bounce_rate   |
|-----|----------------------|----------------|-----------------------|----------------|
|   2 | (direct)             |          19891 |                  8606 |     43.2657986 |
|   3 | youtube.com          |           6351 |                  4238 |    66.72964887 |
|   4 | analytics.google.com |           1972 |                  1064 |    53.95537525 |
|   5 | Partners             |           1788 |                   936 |    52.34899329 |
|   6 | m.facebook.com       |            669 |                   430 |    64.27503737 |
|   7 | google.com           |            368 |                   183 |    49.72826087 |
|   8 | dfa                  |            302 |                   124 |    41.05960265 |
|   9 | sites.google.com     |            230 |                    97 |    42.17391304 |
|  10 | facebook.com         |            191 |                   102 |    53.40314136 |

### Query 04: Average number of pageviews by purchaser type (purchasers vs non-purchasers) in June, July 2017.
- SQL code
  
~~~~sql
with 
purchaser_data as(
  select
      format_date("%Y%m",parse_date("%Y%m%d",date)) as month,
      ROUND((sum(totals.pageviews)/count(distinct fullvisitorid)),7) as avg_pageviews_purchase,
  from `bigquery-public-data.google_analytics_sample.ga_sessions_2017*`
    ,unnest(hits) hits
    ,unnest(product) product
  where _table_suffix between '0601' and '0731'
  and totals.transactions>=1
  and product.productRevenue is not null
  group by month
),

non_purchaser_data as(
  select
      format_date("%Y%m",parse_date("%Y%m%d",date)) as month,
      ROUND(sum(totals.pageviews)/count(distinct fullvisitorid),7) as avg_pageviews_non_purchase,
  from `bigquery-public-data.google_analytics_sample.ga_sessions_2017*`
      ,unnest(hits) hits
    ,unnest(product) product
  where _table_suffix between '0601' and '0731'
  and totals.transactions is null
  and product.productRevenue is null
  group by month
)

select
    pd.*,
    avg_pageviews_non_purchase
from purchaser_data as pd
full join non_purchaser_data using(month)
order by pd.month;
~~~~

- Query result

| Row |  month   |  avg_pageviews_purchase  |  avg_pageviews_non_purchase  |
|-----|----------|--------------------------|------------------------------|
|   1 | 201706   |               94.0205011 |                  316.8655885 | 
|   2 | 201707   |              124.2375519 |                  334.0565598 | 

### Query 05: Average number of transactions per user that made a purchase in July 2017.
- SQL code
  
~~~~sql
select
    format_date("%Y%m",parse_date("%Y%m%d",date)) as month,
    ROUND(sum(totals.transactions)/count(distinct fullvisitorid),9) as Avg_total_transactions_per_user
from `bigquery-public-data.google_analytics_sample.ga_sessions_201707*`
    ,unnest (hits) hits,
    unnest(product) product
where  totals.transactions>=1
and product.productRevenue is not null
group by month;
~~~~

- Query result

| Row |  month   |  Avg_total_transactions_per_user  |
|-----|----------|-----------------------------------|
|   1 | 201707   |                       4.163900415 |
  
### Query 06: Average amount of money spent per session. Only include purchaser data in July 2017
- SQL code
  
~~~~sql
select
    format_date("%Y%m",parse_date("%Y%m%d",date)) as month,
    ((sum(product.productRevenue)/sum(totals.visits))/power(10,6)) as avg_revenue_by_user_per_visit
from `bigquery-public-data.google_analytics_sample.ga_sessions_201707*`
  ,unnest(hits) hits
  ,unnest(product) product
where product.productRevenue is not null
and totals.transactions>=1
group by month;
~~~~

- Query result

| Row |  month   |  avg_revenue_by_user_per_visit    |
|-----|----------|-----------------------------------|
|   1 | 201707   |                43.856598348051243 |

### Query 07: Other products purchased by customers who purchased product "YouTube Men's Vintage Henley" in July 2017. Output should show product name and the quantity was ordered.
- SQL code
  
~~~~sql
with buyer_list as(
    SELECT
        distinct fullVisitorId
    FROM `bigquery-public-data.google_analytics_sample.ga_sessions_201707*`
    , UNNEST(hits) AS hits
    , UNNEST(hits.product) as product
    WHERE product.v2ProductName = "YouTube Men's Vintage Henley"
    AND totals.transactions>=1
    AND product.productRevenue is not null
)

SELECT
  product.v2ProductName AS other_purchased_products,
  SUM(product.productQuantity) AS quantity
FROM `bigquery-public-data.google_analytics_sample.ga_sessions_201707*`
, UNNEST(hits) AS hits
, UNNEST(hits.product) as product
JOIN buyer_list using(fullVisitorId)
WHERE product.v2ProductName != "YouTube Men's Vintage Henley"
 and product.productRevenue is not null
GROUP BY other_purchased_products
ORDER BY quantity DESC;
~~~~

- Query result

| Row |  month   |  Avg_total_transactions_per_user  |
|-----|----------|-----------------------------------|
|   1 | 201707   |                       4.163900415 |


### Query 08: Calculate cohort map from product view to addtocart to purchase in January, February and March 2017. 

- SQL code
~~~~sql
with
product_view as(
  SELECT
    format_date("%Y%m", parse_date("%Y%m%d", date)) as month,
    count(product.productSKU) as num_product_view
  FROM `bigquery-public-data.google_analytics_sample.ga_sessions_*`
  , UNNEST(hits) AS hits
  , UNNEST(hits.product) as product
  WHERE _TABLE_SUFFIX BETWEEN '20170101' AND '20170331'
  AND hits.eCommerceAction.action_type = '2'
  GROUP BY 1
),

add_to_cart as(
  SELECT
    format_date("%Y%m", parse_date("%Y%m%d", date)) as month,
    count(product.productSKU) as num_addtocart
  FROM `bigquery-public-data.google_analytics_sample.ga_sessions_*`
  , UNNEST(hits) AS hits
  , UNNEST(hits.product) as product
  WHERE _TABLE_SUFFIX BETWEEN '20170101' AND '20170331'
  AND hits.eCommerceAction.action_type = '3'
  GROUP BY 1
),

purchase as(
  SELECT
    format_date("%Y%m", parse_date("%Y%m%d", date)) as month,
    count(product.productSKU) as num_purchase
  FROM `bigquery-public-data.google_analytics_sample.ga_sessions_*`
  , UNNEST(hits) AS hits
  , UNNEST(hits.product) as product
  WHERE _TABLE_SUFFIX BETWEEN '20170101' AND '20170331'
  AND hits.eCommerceAction.action_type = '6'
  and product.productRevenue is not null   
  group by 1
)

select
    pv.*,
    num_addtocart,
    num_purchase,
    round(num_addtocart*100/num_product_view,2) as add_to_cart_rate,
    round(num_purchase*100/num_product_view,2) as purchase_rate
from product_view pv
left join add_to_cart a on pv.month = a.month
left join purchase p on pv.month = p.month
order by pv.month;
~~~~

- Query result

| Row |  month   |  num_product_view  |  num_addtocart   |  num_purchase   |  add_to_cart_rate  |  purchase_rate  |
|-----|----------|--------------------|------------------|-----------------|--------------------|-----------------|
|   1 | 201701   |              25787 |             7342 |            2143 |              28.47 |            8.31 |
|   2 | 201702   |              21489 |             7360 |            2060 |              34.25 |            9.59 |
|   3 | 201703   |              23549 |             8782 |            2977 |              37.29 |           12.64 |

# 6. Conclusions
- This is the author's opportunity to learn about the marketing industry and the customer journey through this e-commerce dataset
- In analyzing the e-commerce dataset using BigQuery, the author understands customer behavior through the bounce rate, transaction, revenue, visit, and purchase.
- The author gained insights into which marketing channels drive traffic and sales by examining referral sources. Investing resources in effective channels and optimizing underperforming ones can improve marketing ROI.
- In conclusion, exploring the e-commerce dataset on BigQuery unearthed a wealth of insights critical for strategic decision-making to help the business can optimize operations, enhance customer experiences, and drive revenue.
