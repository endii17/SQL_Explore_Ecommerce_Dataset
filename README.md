# [SQL] Explore Ecommerce Dataset
## I. Introduction
This project contains an eCommerce dataset that I will explore using SQL on [Google BigQuery](https://cloud.google.com/bigquery). The dataset is based on the Google Analytics public dataset and contains data from an eCommerce website.
## II. Requirements
- [Google Cloud Platform account](https://cloud.google.com/?hl=en)
- Project on Google Cloud Platform
- [Google BigQuery API](https://cloud.google.com/bigquery/docs/enable-transfer-service#:~:text=Enable%20the%20BigQuery%20Data%20Transfer%20Service,-Before%20you%20can&text=Open%20the%20BigQuery%20Data%20Transfer,Click%20the%20ENABLE%20button.)
- [SQL query editor](https://cloud.google.com/bigquery)
## III. Dataset Access
The eCommerce dataset is stored in a public Google BigQuery dataset. To access the dataset, follow these steps:
- Log in to your Google Cloud Platform account and create a new project.
- Navigate to the BigQuery console and select your newly created project.
- At the Explorer, search "ga_sessions_" to open it.
## IV. Exploring the Dataset
In this project, I will write 08 queries in Bigquery for this Ecommerce dataset

### Query 01: Calculate total visit, pageview, transaction for January, February and March 2017 (Order by month).
- SQL code
  
  ![Screenshot 2024-07-23 212615](https://github.com/user-attachments/assets/ee988f8c-b087-4025-9586-20d987040c3a)
  
- Query result
  
  ![a2](https://github.com/user-attachments/assets/9a5ab603-1dc4-42f8-bebc-989decf2c045)

### Query 02: Bounce rate per traffic source in July 2017 (Order by total_visit DESC).
- SQL code
  
  ![image](https://github.com/user-attachments/assets/b89722b5-56cc-43ab-98e6-8e6eb09c08b0)
  
- Query result
  
  ![image](https://github.com/user-attachments/assets/63e09b02-c5e9-4726-9de4-31b48f6157fd)

### Query 03: Revenue by traffic source by week, by month in June 2017.
- SQL code
  
  ![image](https://github.com/user-attachments/assets/4e852afd-4df2-4851-9765-559fff329b4a)

- Query result

  ![image](https://github.com/user-attachments/assets/54ca14c8-80ae-4419-81f7-aaaf2824c74b)

### Query 04: Average number of pageviews by purchaser type (purchasers vs non-purchasers) in June, July 2017.
- SQL code
  
  ![image](https://github.com/user-attachments/assets/a8127a1e-01f1-4192-8ccf-e0ea72fbdf15)

- Query result

  ![image](https://github.com/user-attachments/assets/9a158875-54dc-41b6-8a77-e283f43aef58)

### Query 05: Average number of transactions per user that made a purchase in July 2017.
- SQL code
  
  ![image](https://github.com/user-attachments/assets/88ed1a7b-a55b-46d5-af6e-477b19860ba6)

- Query result

  ![image](https://github.com/user-attachments/assets/4cc56359-a482-4841-887a-bd145ca4c5eb)
  
### Query 06: Average amount of money spent per session. Only include purchaser data in July 2017
- SQL code
  
  ![image](https://github.com/user-attachments/assets/d7285372-35e6-424b-9dc3-e59d8ab0c5e1)

- Query result

  ![image](https://github.com/user-attachments/assets/75ef39d7-2223-49cd-a963-43f440b6a729)
