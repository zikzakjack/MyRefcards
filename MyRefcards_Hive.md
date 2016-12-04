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
	
	-- Multiple Partitions by state, city
	CREATE TABLE customers_multiple_partitioned
        (customer_id BIGINT, customer_fname STRING, customer_lname STRING, customer_email STRING, customer_password STRING, customer_street STRING, customer_zipcode STRING)
        PARTITIONED BY (customer_state STRING, customer_city STRING)
        ROW FORMAT DELIMITED
        FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n';

	-- How to prevent full table scan query
	hive> set hive.mapred.mode=strict;
	
	-- How to allow full table scan query
	hive> set hive.mapred.mode=nonstrict;
	
	-- List Partitions of a table
	SHOW PARTITIONS customers_partitioned;
	SHOW PARTITIONS customers_multiple_partitioned;
	
	-- Partition filters
	SHOW PARTITIONS customer PARTITION(country = 'US');
	SHOW PARTITIONS customer PARTITION(country = 'US', state='DC');
	
## Bucketing
	
	-- Enable Buketing
	set hive.enforce.bucketing=true;
	
	CREATE TABLE sales_bucketed (id INT, fname STRING, lname STRING, address STRING,city STRING,state STRING, zip STRING, IP STRING, prod_id STRING, date1 STRING) CLUSTERED BY (id) INTO 10 BUCKETS;
	INSERT INTO sales_bucketed SELECT * from sales;
	

## Beeline

	beeline -u 'jdbc:hive2://localhost:10000/default' -n root -p xxx -d org.apache.hive.jdbc.HiveDriver -e "select * from sales;"
	beeline -u 'jdbc:hive2://localhost:10000/default' -n cloudera -p cloudera -d org.apache.hive.jdbc.HiveDriver -e "select * from sales;"
	

## Hive cli

