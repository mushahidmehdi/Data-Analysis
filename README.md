
# Data Analysis - Fetch Rewards Coding Exercise 
In this project we will demonstrate how to understand data and relate one data set to other to answer predetermine bussiness question.

There are various methods we load the data into database:


###### 1- Writing SQL dialect patriculay related to the RBMS in used in my case PostgreSQL.
###### 2- Traditional way of uploading data into database using Python
(JSON-Data-Analysis-in-Python https://github.com/mushahidmehdi/JSON-Data-Analysis-in-Python/edit/main/README.md in this repo we will perform exactly same task but using Python Functions)


## In This Project we will use PostgreSQL dilects to genrate RDBMS

### STEPS:

1- Review unstructure json data and build a new structure relational data base in PostgreSQL using Postgres Dilects.                                                 
2- Generate query to answer predetermine bussiness question.                                                                                          
3- Write a short Email to bussiness stack holder about predertmined questions.                                                                                         

We have three different json data.

    fetchdb=# CREATE VIEW rewards_view AS
    
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




