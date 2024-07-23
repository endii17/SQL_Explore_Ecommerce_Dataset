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

### Query 01: Calculate total visit, pageview, transaction for Jan, Feb and March 2017 (Order by month)
- SQL code
  
  ![Screenshot 2024-07-23 212615](https://github.com/user-attachments/assets/ee988f8c-b087-4025-9586-20d987040c3a)
- Query result
  
  ![a2](https://github.com/user-attachments/assets/9a5ab603-1dc4-42f8-bebc-989decf2c045)

