
![GitHub repo size](https://img.shields.io/github/repo-size/mushahidmehdi/Data-Analysis-Using-PostgreSQL-dialects?style=plastic)
![Read the Docs](https://img.shields.io/readthedocs/pip?style=plastic)
![GitHub commit merge status](https://img.shields.io/github/commit-status/mushahidmehdi/Full-Stack-Web-Application/main/c49a9cf916c11d163b7b4d1256b89c211793d6ee)

![Conda](https://img.shields.io/conda/pn/conda-forge/python)



# Data Analysis - Fetch Rewards Coding Exercise 
In this project we will demonstrate how to understand data and relate one data set to other to answer predetermine bussiness question.

There are various methods we load the data into database:


###### 1- Writing SQL dialect patriculay related to the RBMS in used in my case PostgreSQL.
###### 2- Traditional way of uploading data into database using Python

JSON-Data-Analysis-in-Python in this repo we will perform exactly same task but using Python Functions                                                             
https://github.com/mushahidmehdi/JSON-Data-Analysis-in-Python/README.md

## In This Project we will use PostgreSQL dilects to genrate RDBMS

### STEPS:

1- Review unstructure json data and build a new structure relational data base in PostgreSQL using Postgres Dilects.                                                 
2- Generate query to answer predetermine bussiness question.                                                                                          
3- Write a short Email to bussiness stack holder about predertmined questions.                                                                                         

We have three different json data.

##### 1- users.json
##### 2- brands.json
##### 3- receipts.json


###### Now lets create a database tables for all the above json data

![receipts-users-brands](https://user-images.githubusercontent.com/66418035/122520611-7ecda480-d01c-11eb-96d3-e88e39a9c29f.png)

###### Lets upload the json data into the database through python with psycpg2 

![loading-data-into-database](https://user-images.githubusercontent.com/66418035/122520740-ab81bc00-d01c-11eb-86ef-d2075cd19f74.png)



###### Lets create a view for users Tables


    fetchdb=# CREATE VIEW user_view AS 
    SELECT
    DATA -> '_id' ->> '$oid' AS _id,
    DATA ->> 'active' AS active,
    DATA -> 'createdDate' ->> '$date' AS createddate ,
    DATA -> 'lastLogin' ->> '$date' AS lastlogin,
    DATA ->> 'role' AS role,
    DATA ->> 'signUpSource' AS signupsource,
    DATA ->> 'state' AS state
    fetchdb-# FROM users;
    
 ![user-view](https://user-images.githubusercontent.com/66418035/122521241-42e70f00-d01d-11eb-84a9-bc9887a35beb.png)


###### Create a view for brands Tables


    fetchdb=# CREATE VIEW brands_view AS
    SELECT
    DATA -> '_id' ->> '$oid' AS _id,
    DATA ->> 'barcode' AS barcode,
    DATA ->> 'category' AS category,
    DATA ->> 'categoryCode' AS category_code,
    DATA -> 'cpg' -> '$oid' ->> '$oid' AS cpg_id,
    DATA -> 'cpg' ->> '$ref' AS cpg_ref,
    DATA ->> 'name' AS name,
    DATA ->> 'topBrand' AS topbrand 
    FROM brands;

![brands_view](https://user-images.githubusercontent.com/66418035/122521273-4da1a400-d01d-11eb-9a22-a904123053f0.png)




###### Create a view for receipts Tables
    
    fetchdb=# CREATE VIEW receipts_view AS
    SELECT
    DATA -> '_id' ->> '$oid' AS id,
    DATA ->> 'bonusPointsEarned' AS bonus_points_earned,
    DATA ->> 'bonusPointsEarnedReason' AS bonus_points_earned_reason,
    DATA -> 'createDate' ->> '$date' AS create_date, 
    DATA -> 'dateScanned' ->> '$date'  AS date_scanned,
    DATA -> 'finishedDate' ->> '$date' AS finished_date,
    DATA -> 'modifyDate' ->> '$date' AS modify_date,
    DATA -> 'pointsAwardedDate' ->> '$date' AS points_award_date,
    DATA -> 'pointsEarned' ->> '$date' AS points_earned,
    DATA -> 'purchaseDate' ->> '$date' AS purchase_date,
    DATA ->> 'purchasedItemCount' AS purchased_item_count,
    DATA ->> 'rewardsReceiptStatus' AS rewards_receipt_status,
    DATA ->> 'totalSpent' AS total_spent,
    DATA ->> 'userId' AS user_id
    FROM receipts;
    
    
![receipts-view](https://user-images.githubusercontent.com/66418035/122521303-55f9df00-d01d-11eb-9a09-068b2a7f1704.png)
    
    
    
   
    
###### Create a view for rewards Tables from the list within receipts:
    
    SELECT 
    DATA -> '_id' ->> '$oid' AS _id,
    jsonb_array_elements(DATA -> 'rewardsReceiptItemList') ->> 'barcode' AS barcode,
    jsonb_array_elements(DATA -> 'rewardsReceiptItemList') ->> 'description' as description,
    jsonb_array_elements(DATA -> 'rewardsReceiptItemList') ->> 'finalPrice' as final_price,
    jsonb_array_elements(DATA -> 'rewardsReceiptItemList') ->> 'itemPrice' as item_price,
    jsonb_array_elements(DATA -> 'rewardsReceiptItemList') ->> 'needsFetchReview' as needs_fetch_review,
    jsonb_array_elements(DATA -> 'rewardsReceiptItemList') ->> 'partnerItemId' AS partner_item_id,
    jsonb_array_elements(DATA -> 'rewardsReceiptItemList') ->> 'preventTargetGapPoints' AS prevent_target_gap_points,
    jsonb_array_elements(DATA -> 'rewardsReceiptItemList') ->> 'quantityPurchased' AS quantity_purchased,
    jsonb_array_elements(DATA -> 'rewardsReceiptItemList') ->> 'userFlaggedBarcode' AS user_flagged_barcode,
    jsonb_array_elements(DATA -> 'rewardsReceiptItemList') ->> 'userFlaggedNewItem' AS user_flagged_new_item,
    jsonb_array_elements(DATA -> 'rewardsReceiptItemList') ->> 'userFlaggedPrice' AS user_flagged_price,
    jsonb_array_elements(DATA -> 'rewardsReceiptItemList') ->> 'userFlaggedQuantity' AS user_flagged_quantity
    from receipts;

   
![rewards-view](https://user-images.githubusercontent.com/66418035/122521323-5e521a00-d01d-11eb-8560-46914d487a66.png)




