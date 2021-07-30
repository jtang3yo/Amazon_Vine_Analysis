# Pet Products - Amazon_Vine_Analysis
## Overview of Project
  The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review. In this project, you’ll have access to approximately 50 datasets. Each one contains reviews of a specific product, from clothing apparel to wireless products. You’ll need to pick one of these datasets and use PySpark to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. Next, you’ll use PySpark, Pandas, or SQL to determine if there is any bias toward favorable reviews from Vine members in your dataset. Then, you’ll write a summary of the analysis for Jennifer to submit to the SellBy stakeholders.

## Deliverables: 
This new assignment consists of two technical analysis deliverables and a written report.
  1. Deliverable 1: Perform ETL on Amazon Product Reviews
  2. Deliverable 2: Determine Bias of Vine Reviews

### Data Source, Resources and Software
  1. Data Source: SQL table schema.csv and Amazon ETL starter code.csv
  2. Data Tools: Amazon_Reviews_ETL.ipynb and Vine_Review_Analysis.ipynb.
  3. Software: Python 3.9, Visual Studio Code 1.50.0, Anaconda 4.8.5, Jupyter Notebook 6.1.4 and Pandas, Google Colab Notebook, Amazon Web Services (RDS, S3),                postgreSQL, pgAdmin, PySpark 
 
### Devlierbale 1: Amazon_Review_Analysis
  1. From the following Amazon Review datasets, pick [pet products dataset] (https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Pet_Products_v1_00.tsv.gz) to analyze. All the datasets have the same schemata, as shown in this image: <img width="1203" alt="load aws s3 pet products dataset " src="https://user-images.githubusercontent.com/82353749/127679938-5b2b9675-a1c3-4446-90a7-f366a28628fe.png">

  2. In pgAdmin, create a new database in your Amazon RDS server that you just create.

  3. After loading the dataset in Colab environment, **customers_table DataFrame**
  To create the customers_table, use the groupby() function on the customer_id column of the DataFrame, count all the customer ids using the agg() function by chaining it to the groupby() function. After using this function, a new column will be created, count(customer_id), and rename the count(customer_id) column using the withColumnRenamed() function so it matches the schema for the customers_table in pgAdmin. The final customer_table dataframe shown as: 
    <img width="1175" alt="customers_df" src="https://user-images.githubusercontent.com/82353749/127680719-104372f0-c606-4211-a3ec-969f933d528c.png">

  4. **Product_table DataFrame** 
  To Create products_table, use the select() function to select the product_id and product_title, then drop duplicates with the drop_duplicates() function to retrieve only unique product_ids. Refer to the code snippet provided in the Amazon_Reviews_ETL_starter_code.ipynb file for assistance. The final products_table dataframe shwon as: 
    <img width="796" alt="products_df" src="https://user-images.githubusercontent.com/82353749/127681088-c958d784-7b52-4ef8-8466-e97aff7edd7a.png">
  
  5. **review_id_table DataFrame**
  To create review_id_table, use the select() function to select the columns that are in the review_id_table in pgAdmin, and convert the review_date column to a date using pyspark.sql.functions import to_date function. The final review_id_table shown as: 
    <img width="1180" alt="review_id_table_df" src="https://user-images.githubusercontent.com/82353749/127681457-16c1fabb-42e0-4fdd-9e30-50c802c996e2.png">

  6. **Vine_table DataFrame**
  To create vine_table, use the select() function to select only the columns that are in the vine_table in pgAdmin. 
    <img width="960" alt="vine_df" src="https://user-images.githubusercontent.com/82353749/127681664-cf874ff5-bfc2-4ba1-b8c7-b0b87d46809f.png">

  7. Connect to the AWS RDS instance and write each DataFrame to its table. 
     ** Configure settings for RDS: <img width="1182" alt="configure RDS" src="https://user-images.githubusercontent.com/82353749/127681999-9b20a3b2-8b89-4c0e-b152-8d8c271da788.png">
     ** customers table: <img width="1339" alt="cutomers_table" src="https://user-images.githubusercontent.com/82353749/127680047-5ab80e7e-1a36-49d3-b730-5c4f8f375912.png">
     ** products table: <img width="1340" alt="products_table" src="https://user-images.githubusercontent.com/82353749/127680057-3793cfb9-9fde-4382-9461-2b08f472e014.png">
     ** review_id table: <img width="1339" alt="review_id_table" src="https://user-images.githubusercontent.com/82353749/127680110-1d03a07d-9d1b-40bd-895a-e9c9552446f7.png">
     ** vine_table: <img width="1340" alt="vine_table" src="https://user-images.githubusercontent.com/82353749/127680129-c6910646-b386-4b38-b2fe-c8db76897733.png">
     
### Deliverable 2: Vine_Review_Analysis
   1. Filter the data and create a new DataFrame or table to retrieve all the rows where the total_votes count is equal to or greater than 20 to pick reviews
    <img width="1178" alt="Screen Shot 2021-07-30 at 12 23 01 PM" src="https://user-images.githubusercontent.com/82353749/127682735-ba78eda6-8de4-40de-9058-8958822b6e68.png">
    2. 2.Filter the new DataFrame or table created in Step 1 and create a new DataFrame or table to retrieve all the rows where the number of helpful_votes divided by total_votes is equal to or greater than 50%.
    <img width="1184" alt="Screen Shot 2021-07-30 at 12 26 35 PM" src="https://user-images.githubusercontent.com/82353749/127683134-e077bccf-9d6d-429d-8a42-8e5be1bd7060.png">
    3. Filter the DataFrame or table created in Step 2, and create a new DataFrame or table that retrieves all the rows where a review was written as part of the Vine program (paid), vine == 'Y'
    <img width="1183" alt="Screen Shot 2021-07-30 at 12 27 46 PM" src="https://user-images.githubusercontent.com/82353749/127683377-5aec2d33-c1ab-48da-bff9-efb3ca381874.png">
    4. Repeat Step 3, but this time retrieve all the rows where the review was not part of the Vine program (unpaid), vine == 'N'
    <img width="1175" alt="Screen Shot 2021-07-30 at 12 29 38 PM" src="https://user-images.githubusercontent.com/82353749/127683508-ddc2a1ae-b46b-4966-9e79-fd7827a6a6c5.png">
    5. Determine the total number of reviews, the number of 5-star reviews, and the percentage of 5-star reviews for the two types of review (paid vs unpaid).
    <img width="1176" alt="Screen Shot 2021-07-30 at 12 30 45 PM" src="https://user-images.githubusercontent.com/82353749/127683683-eab9bce4-99d5-467c-b653-69b7ee64b05b.png">
    <img width="1171" alt="Screen Shot 2021-07-30 at 12 31 54 PM" src="https://user-images.githubusercontent.com/82353749/127683781-58e65f81-8d53-4c34-b7ef-3ecf19b3218a.png">
    <img width="1189" alt="Screen Shot 2021-07-30 at 12 32 57 PM" src="https://user-images.githubusercontent.com/82353749/127683975-f7f590a2-ade6-4f6a-b984-90496024504e.png">
    <img width="1197" alt="Screen Shot 2021-07-30 at 12 34 28 PM" src="https://user-images.githubusercontent.com/82353749/127684060-f87fb681-db0d-4dd8-ba9f-5f3b33ab9368.png">
    <img width="1200" alt="Screen Shot 2021-07-30 at 12 35 34 PM" src="https://user-images.githubusercontent.com/82353749/127684190-ef61b60c-0430-4273-be20-5bb94fa89613.png">
    <img width="1117" alt="Screen Shot 2021-07-30 at 12 36 23 PM" src="https://user-images.githubusercontent.com/82353749/127684295-3c08a1f1-3979-43f7-9ef4-e98fb8eb86b3.png">

## Summary: Deliverable Results 

 1. How many Vine reviews and non-Vine reviews were there?

 **Total Vine Review: 10,215**
 
 **Total Non-Vine Review: 2,633,399**
 
 2. How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?

 **Vine 5 stars Review: 4343**
 
 **Non-Vine 5 stars Review: 1,641,210**
 
 3. What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?

 **% of Vine 5 stars Review: 42.5%**
 
 **% of Non-Vine 5 stars Review: 63.3%**
 
 <img width="805" alt="Screen Shot 2021-07-30 at 2 58 48 PM" src="https://user-images.githubusercontent.com/82353749/127699719-78a0f5cc-a2a6-436f-bc9a-7e3cab9952e8.png">










  
