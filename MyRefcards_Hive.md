# Hive

## References

###### 1. [Hive Documentation](https://cwiki.apache.org/confluence/display/Hive/Home)
###### 2. [Programming Hive by Edward Capriolo, Dean Wampler, and Jason Rutherglen � O'Reilly Media](http://shop.oreilly.com/product/0636920023555.do)

## Data Types

1. Numeric Data Types
	* TINYINT			e.g., 
	* SMALLINT			e.g., 
	* INT				e.g., 
	* BIGINT			e.g., 
	* FLOAT				e.g., 
	* DOUBLE			e.g., 
	* DECIMAL			e.g., 
2. String Data Types
	* STRING			e.g., 
	* VARCHAR			e.g., 
	* CHAR				e.g., 
3. Date/Time Data Types
	* DATE				e.g., 
	* TIMESTAMP			e.g., 
	* bytearray			e.g., 
4. Misc Data Types
	* BOOLEAN			e.g., 
	* BINARY			e.g., 
5. Complex Types
	* STRUCT			e.g., 
	* MAP				e.g., 
	* ARRAY				e.g., 
	
## Operators

1. Arithmetic Operators
	* A + B
	* A - B
	* A * B
	* A / B
	* A % B
	* A & B
	* A | B
	* A ^ B
	* ~B
2. Relational Operators
	* A = B
	* A != B
	* A <=> B
	* A <> B
	* A < B
	* A <= B
	* A > B
	* A >= B
	* A BETWEEN B AND C
	* A NOT BETWEEN B AND C
	* A IS NULL
	* A IS NOT NULL
	* A LIKE B
	* A NOT LIKE B
	* A RLIKE B
	* A REGEXP B
3. Logical Operators
	* A AND B
	* A && B
	* A OR B
	* A || B
	* NOT A
	* !A
	* A IN (value1, value2, …)
	* A IN (SUBQUERY)
	* A NOT IN (value1, value2, …)
	* A NOT IN (subquery)
	* EXISTS (subquery)
	* NOT EXISTS (subquery)
4. Complex Operators
	* A[i]
	* M[key]
	* S.a
	
## Hive Data Definition Language
	
### Creating a database schema

	CREATE DATABASE retail_dba LOCATION '/user/hive/warehouse/retail_dba/';
	
### Dropping a database schema

	-- Drop Database. Error will be thrown if the database does not exist
	Drop database retail_dba;
	
	-- Drop Database. Error will not be thrown if the database does not exist
	Drop database if exists retail_dba;
	
	-- Drop Database. Error will be thrown if the database is not empty
	Drop database if exists retail_dba restrict;
	
	-- Drop Database. if the database is not empty, all tables are dropped before dropping the database
	Drop database if exists retail_dba cascade;
	
	
### Altering a database schema

	Alter database retail_dba set dbproperties ('Created by' = 'zik-zak-jack', 'Created on' = '04-Dec-2016');
	
### Using a database schema
	
	Use retail_dba;
	
### Showing database schemas

	Show databases;
	
### Describing a database schema

	Describe schema retail_dba;
	
	Describe schema extended retail_dba;
	
	
### Creating tables

	    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table customers \
        --fields-terminated-by \\t \
        --warehouse-dir=/user/hive/warehouse/retail_dba
        
        show databases;
        use retail_dba;
        
        create external table customers 
        (customer_id BIGINT, customer_fname STRING, customer_lname STRING, customer_email STRING, customer_password STRING, customer_street STRING, customer_city STRING, customer_state STRING, customer_zipcode STRING)
        ROW FORMAT DELIMITED
        FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        LOCATION '/user/hive/warehouse/retail_dba/customers';
	
### Dropping tables

	-- data is saved into the Trash folder
	Drop table if exists customers;
	
	-- data is not saved into the Trash folder and lost forever
	Drop table if exists customers purge;
	
### Truncating tables

	Truncate table customers;
	
### Renaming tables

	ALTER TABLE customers RENAME TO customers_sav_20161204;
	ALTER TABLE customers_sav_20161204 RENAME TO customers;
	
### Altering table properties

	Alter Table customers_sav_20161204 SET TBLPROPERTIES ('comment' = 'This is a backup for 2016-12-04 data');
	
### Creating views

	Create view customers_full_view As select * from customers;
	Create view if not exists customers_CA AS select customer_id, customer_fname, customer_lname, customer_street, customer_city from customers Where customer_state = 'CA';

### Dropping views

	Drop view customers_full_view;
	
### Altering the view properties

	Alter View customers_CA SET TBLPROPERTIES ('comment' = 'California Customers');
	
### Altering the view as select

	alter view customers_CA as select customer_id, customer_street, customer_city from customers;
	
### Showing tables

	Show tables;
	Show tables in retail_dba;
	Show tables 'cus*';
	
### Showing partitions

	Show partitions customers;
	Show partitions Sales partition(dop='2015-01-01');
	
	
### Show the table properties

	Show tblproperties Sales;
	
### Showing create table

	Show create table customers;
	
### Creating partitions

	Partitioning in Hive is used to increase query performance. Partitions are like horizontal slices of data that allows the large sets of data as more manageable chunks.
	
	-- Partition by state
	CREATE TABLE customers_partitioned
        (customer_id BIGINT, customer_fname STRING, customer_lname STRING, customer_email STRING, customer_password STRING, customer_street STRING, customer_city STRING, customer_zipcode STRING)
        PARTITIONED BY (customer_state STRING)
        ROW FORMAT DELIMITED
        FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n';
	
	insert into customers_partitioned PARTITION (customer_state) select customer_id , customer_fname , customer_lname , customer_email , customer_password , customer_street , customer_city , customer_zipcode, customer_state from customers;
	
	-- Multiple Partitions by state, city
	CREATE TABLE customers_multiple_partitioned
        (customer_id BIGINT, customer_fname STRING, customer_lname STRING, customer_email STRING, customer_password STRING, customer_street STRING, customer_zipcode STRING)
        PARTITIONED BY (customer_state STRING, customer_city STRING)
        ROW FORMAT DELIMITED
        FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n';

	insert into customers_multiple_partitioned PARTITION (customer_state, customer_city) select customer_id , customer_fname , customer_lname , customer_email , customer_password , customer_street  , customer_zipcode, customer_state, customer_city from customers;

	-- How to prevent full table scan query
	hive> set hive.mapred.mode=strict;
	
	-- How to allow full table scan query
	hive> set hive.mapred.mode=nonstrict;
	
	-- to allow dynamic partitions insert
	hive> hive.exec.dynamic.partition=true;
	
	-- default is strict which requires atleast one static partition to be present
	hive> set hive.exec.dynamic.partition.mode=nonstrict;
	
	-- max partitions that can be created by mapper or reducer per node
	hive>set hive.exec.max.dynamic.partitions.pernode=1000;
	
	-- max partitions that can be created
	hive> set hive.exec.max.dynamic.partitions=10000;
	
	-- List Partitions of a table
	SHOW PARTITIONS customers_partitioned;
	SHOW PARTITIONS customers_multiple_partitioned;
	
	-- Partition filters
	SHOW PARTITIONS customer PARTITION(country = 'US');
	SHOW PARTITIONS customer PARTITION(country = 'US', state='DC');
	
### Bucketing
	
	-- Enable Bucketing
	set hive.enforce.bucketing=true;
	
	DROP TABLE customers_bucketed

        CREATE TABLE customers_bucketed (customer_id BIGINT, customer_fname STRING, customer_lname STRING, customer_email STRING, customer_password STRING, customer_street STRING, customer_city STRING, customer_state STRING, customer_zipcode STRING) 
        CLUSTERED BY (customer_id) INTO 5 BUCKETS
        ROW FORMAT DELIMITED
        FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n';

	INSERT INTO customers_bucketed SELECT * from customers;
	
## Data Manipulation Language
	
	-- prep test data
	-- 1. export the data to hdfs

	sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table categories  \
        --fields-terminated-by \\t \
        --warehouse-dir=/user/cloudera/zikzakjack/data/retail_db/
	
	-- 2. copy the data to local filesystem
	
	hdfs dfs -copyToLocal /user/cloudera/zikzakjack/data/retail_db/categories/part-m-00000 /home/cloudera/ZikZakJack/retail_db/categories.txt
	
	-- verify the local file
	cat /home/cloudera/ZikZakJack/retail_db/categories.txt
	
	-- 3. create the table structure in hive
	
	CREATE TABLE categories
        (category_id BIGINT, category_department_id BIGINT, category_name STRING)
        ROW FORMAT DELIMITED
        FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n';
	
### Loading files into tables
	
	-- load data from local file to Hive table
	cat /home/cloudera/ZikZakJack/retail_db/categories.txt
	wc -l /home/cloudera/ZikZakJack/retail_db/categories.txt
	hive> describe categories;
	hive> LOAD DATA LOCAL INPATH '/home/cloudera/ZikZakJack/retail_db/categories.txt' INTO TABLE categories;
	hdfs dfs -ls /user/hive/warehouse/categories/
	hive> select count(*) from categories;
	hive> truncate table categories;
	
	-- load data from hdfs file to Hive table
	hdfs dfs -ls /user/cloudera/zikzakjack/data/retail_db/categories/part-m-00000
	hive> describe categories;
	hive> LOAD DATA INPATH '/user/cloudera/zikzakjack/data/retail_db/categories/part-m-00000' INTO TABLE categories;
	hdfs dfs -ls /user/hive/warehouse/categories/
	hive> select count(*) from categories;

	-- overwrite the data present in the categories
	hive> select count(*) from categories;
	hive> LOAD DATA LOCAL INPATH '/home/cloudera/ZikZakJack/retail_db/categories.txt' OVERWRITE INTO TABLE categories;
	hive> select count(*) from categories;

	
### Inserting data into Hive tables from queries
	
	CREATE TABLE categories_copy AS SELECT * FROM categories WHERE 1=0;
	select count(*) from categories_copy;
	INSERT INTO categories_copy SELECT * FROM categories;
	select count(*) from categories_copy;
	SELECT count(*) FROM categories WHERE category_department_id = 6;
	INSERT INTO categories_copy SELECT * FROM categories WHERE category_department_id = 6;
	select count(*) from categories_copy;
	INSERT OVERWRITE TABLE categories_copy SELECT * FROM categories;
	select count(*) from categories_copy;
	INSERT OVERWRITE TABLE categories_copy SELECT * FROM categories WHERE category_id = 1;
	select count(*) from categories_copy;
	
### Inserting data into dynamic partitions
	
	CREATE TABLE customers_partitioned_01
        (customer_id BIGINT, customer_fname STRING, customer_lname STRING, customer_email STRING, customer_password STRING, customer_street STRING, customer_city STRING, customer_zipcode STRING)
        PARTITIONED BY (customer_state STRING)
        ROW FORMAT DELIMITED
        FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n';
	
	FROM customers_bucketed cust INSERT OVERWRITE TABLE customers_partitioned_01 PARTITION(customer_state) select cust.customer_id , cust.customer_fname , cust.customer_lname , cust.customer_email , cust.customer_password , cust.customer_street , cust.customer_city, cust.customer_zipcode, customer_state;
	
	select count(*) from customers_partitioned_01;
	
	CREATE TABLE customers_multiple_partitioned_01
        (customer_id BIGINT, customer_fname STRING, customer_lname STRING, customer_email STRING, customer_password STRING, customer_street STRING, customer_zipcode STRING)
        PARTITIONED BY (customer_state STRING, customer_city STRING)
        ROW FORMAT DELIMITED
        FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n';

	FROM customers_bucketed cust INSERT OVERWRITE TABLE customers_multiple_partitioned_01 PARTITION(customer_state, customer_city) select cust.customer_id , cust.customer_fname , cust.customer_lname , cust.customer_email , cust.customer_password , cust.customer_street , cust.customer_city, cust.customer_zipcode, customer_state;

	select count(*) from customers_multiple_partitioned_01;
	
### Writing data into files from queries
	
	
### Enabling transactions in Hive
	
	
### Inserting values into tables from SQL
	
	
### Updating data
	
	
### Deleting data
	
	

## Beeline

	beeline -u 'jdbc:hive2://localhost:10000/default' -n root -p xxx -d org.apache.hive.jdbc.HiveDriver -e "select * from sales;"
	beeline -u 'jdbc:hive2://localhost:10000/default' -n cloudera -p cloudera -d org.apache.hive.jdbc.HiveDriver -e "select * from sales;"
	

## Hive cli

