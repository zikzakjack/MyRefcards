# Sqoop

## References

###### 1. [Sqoop User Guide](http://sqoop.apache.org/docs/1.4.6/SqoopUserGuide.html)
###### 2. [Apache Sqoop Cookbook by Kathleen Ting and Jarek Jarcec Cecho (O�Reilly). Copyright 2013 Kathleen Ting and Jarek Jarcec Cecho, 978-1-449-36462-5](https://www.amazon.com/Apache-Sqoop-Cookbook-Unlocking-Relational/dp/1449364624)

## Help

sqoop help

## Version

sqoop version

## List Databases

    sqoop list-databases \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --verbose

## List Tables

    sqoop list-tables \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --verbose

## Provide Password from Command Prompt

    sqoop list-tables \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        -P

## Import Sqoop Password File into HDFS

    echo -n "cloudera" > sqoop.password
    hdfs dfs -put sqoop.password /user/cloudera/sqoop.password
    hdfs dfs -chown 400 /user/cloudera/sqoop.password
    rm sqoop.password

## Provide Password from a Password File

    sqoop list-tables \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password-file sqoop.password

## Import a Table

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --fields-terminated-by \\t \
        --warehouse-dir=/user/hive/warehouse
    
## Import a Table in SequenceFile format

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --target-dir=/user/hive/warehouse/departments_ff_sq \
        --as-sequencefile
    
## Import a Table in Avro File format

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --target-dir=/user/hive/warehouse/departments_ff_avro \
        --as-avrodatafile
    
## Import a Table in Parquet File format

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --target-dir=/user/hive/warehouse/departments_ff_parquet \
        --as-parquetfile
    
## Import a Table in GZip compressed format

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --fields-terminated-by \\t \
        --target-dir=/user/hive/warehouse/departments_compressed_GZip \
        --compress
    
## Import a Table in BZip2 compressed format

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --fields-terminated-by \\t \
        --target-dir=/user/hive/warehouse/departments_compressed_BZip2 \
        --compress \
        --compression-codec org.apache.hadoop.io.compress.BZip2Codec
    
## Import only a sub-set of Table data

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --where "department_id >= 5" \
        --fields-terminated-by \\t \
        --target-dir=/user/hive/warehouse/departments_gt_5
    
## Override Column Type Mapping

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --fields-terminated-by \\t \
        --target-dir=/user/hive/warehouse/departments_col_mapping \
        --map-column-java department_id=Long,department_name=String
    
## Increasing the Number Of Mappers For Larger Dataset

    sqoop import \
        -m 10 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --fields-terminated-by \\t \
        --target-dir=/user/hive/warehouse/departments_10_mappers
    
## Handling NULL Values From Database

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --target-dir=/user/hive/warehouse/departments_NULL_handling \
        --fields-terminated-by \\t \
        --null-string '\\N' \
        --null-non-string '\\N'
    
## Bulk Import All Tables

    sqoop import-all-tables \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --fields-terminated-by \\t \
        --warehouse-dir=/user/hive/warehouse/import_all
    
## Exclude Tables During Bulk Import

    sqoop import-all-tables \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --fields-terminated-by \\t \
        --warehouse-dir=/user/hive/warehouse/import_all_with_excludes \
        --exclude-tables orders,customers
    
## Importing Only New Data Based On ID Column Value

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table orders \
        --where "order_id <= 4000" \
        --fields-terminated-by \\t \
        --target-dir=/user/hive/warehouse/orders_incremental_append

    sqoop import \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table orders \
        --fields-terminated-by \\t \
        --target-dir=/user/hive/warehouse/orders_incremental_append \
        --incremental=append \
        --check-column=order_id \
        --last-value=4000
    
## Importing Only New Data Based On LastModified Timestamp

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table orders \
        --where "order_date < '2013-08-17 00:00:00'" \
        --fields-terminated-by \\t \
        --target-dir=/user/hive/warehouse/orders_incremental_lastmodified
    
    sqoop import \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table orders \
        --fields-terminated-by \\t \
        --target-dir=/user/hive/warehouse/orders_incremental_lastmodified \
        --incremental=lastmodified \
        --check-column=order_date \
        --last-value='2013-08-17 00:00:00' \
        --merge-key=order_id
    
## Create a Sqoop Job For Incremental Import

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table orders \
        --fields-terminated-by \\t \
        --where "order_date < '2013-08-17 00:00:00'" \
        --target-dir=/user/hive/warehouse/sqoop_job_incremental_import_Orders
    
    sqoop job \
        --create sqoop_job_incremental_import_Orders \
        -- \
        import \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password-file sqoop.password \
        --table orders \
        --fields-terminated-by \\t \
        --target-dir=/user/hive/warehouse/sqoop_job_incremental_import_Orders \
        --incremental=lastmodified \
        --check-column=order_date \
        --last-value='2013-08-17 00:00:00' \
        --merge-key=order_id
    
## List All Sqoop Jobs
    
    sqoop job --list
    
## View a Sqoop Job Definition
    
    sqoop job --show sqoop_job_incremental_import_Orders
    
## Execute a Sqoop Job
    
    sqoop job --exec sqoop_job_incremental_import_Orders
    
## Delete a Sqoop Job
    
    sqoop job --delete sqoop_job_incremental_import_Orders
    
## Add Verbose to Sqoop Job
    
    sqoop job --exec sqoop_job_incremental_import_Orders -- --verbose
    
## Start a Sqoop Metastore Service
    
######    sqoop metastore
    
## Import Data Using a Join Query
    
    sqoop import \
        --num-mappers 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --query 'SELECT cat.category_id as category_id, dept.department_name as department_name, cat.category_name as category_name
            FROM categories cat JOIN departments dept 
            on cat.category_department_id = dept.department_id where $CONDITIONS' \
        --split-by category_id \
        --fields-terminated-by \\t \
        --target-dir=/user/hive/warehouse/categories_denormed \
        --map-column-java category_id=Long,department_name=String,category_name=String
    
## Import Data Using a Join Query and Boundary Conditions
    
    sqoop import \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --query 'SELECT cat.category_id as category_id, dept.department_name as department_name, cat.category_name as category_name
            FROM categories cat JOIN departments dept 
            on cat.category_department_id = dept.department_id where $CONDITIONS' \
        --split-by category_id \
        --boundary-query "select min(category_id), max(category_id) from categories" \
        --fields-terminated-by \\t \
        --target-dir=/user/hive/warehouse/categories_denormed_with_boundary 
    
## Provide Custom Name to MapReduce Jobs triggered by Sqoop

    sqoop import \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --target-dir=/user/hive/warehouse/departments_custom_mr_job \
        --fields-terminated-by \\t \
        --mapreduce-job-name `date +%Y-%m-%d`_`echo $USER`_departments_custom_mr_job_name
    
## MySql RunBook for Cloudera retail_db

######    mysql --user=retail_dba --password=cloudera --database=retail_db
######    
######    TRUNCATE orders_copy_01;
######    TRUNCATE orders_copy_02;
######    TRUNCATE orders_copy_03;
######    TRUNCATE orders_copy_04;
######    TRUNCATE orders_copy_05;
######    TRUNCATE orders_copy_06;
######    TRUNCATE orders_copy_07;
######    TRUNCATE orders_copy_08;
######    TRUNCATE orders_processed;

######    DROP TABLE orders_copy_01;
######    DROP TABLE orders_copy_02;
######    DROP TABLE orders_copy_03;
######    DROP TABLE orders_copy_04;
######    DROP TABLE orders_copy_05;
######    DROP TABLE orders_copy_06;
######    DROP TABLE orders_copy_07;
######    DROP TABLE orders_copy_08;
######    DROP TABLE orders_processed;

######    SELECT count(*) FROM orders; -- 68883
######    CREATE TABLE orders_staging SELECT * FROM orders WHERE 1=0;
######    CREATE TABLE orders_copy_01 SELECT * FROM orders WHERE 1=0;
######    CREATE TABLE orders_copy_02 SELECT * FROM orders WHERE 1=0;
######    CREATE TABLE orders_copy_03 SELECT * FROM orders WHERE 1=0;
######    CREATE TABLE orders_copy_04 SELECT * FROM orders WHERE 1=0;
######    CREATE TABLE orders_copy_05 SELECT * FROM orders WHERE 1=0;
######    CREATE TABLE orders_copy_06 SELECT * FROM orders WHERE order_id <= 100; -- 68783
######    CREATE TABLE orders_copy_07 SELECT * FROM orders WHERE order_id <= 100; -- 68783
######    SELECT * FROM orders_copy_07 where order_id=100;
######    UPDATE orders_copy_07 SET order_status='COMPLETE' where order_id=100;
######    SELECT * FROM orders_copy_07 where order_id=100;
######    CREATE TABLE orders_copy_08 SELECT * FROM orders WHERE 1=0;
######    CREATE TABLE orders_processed SELECT * FROM orders WHERE 1=0;

######    SELECT count(*) FROM orders_staging;
######    SELECT count(*) FROM orders_copy_01;
######    SELECT count(*) FROM orders_copy_02;
######    SELECT count(*) FROM orders_copy_03;
######    SELECT count(*) FROM orders_copy_04;
######    SELECT count(*) FROM orders_copy_05;
######    SELECT count(*) FROM orders_copy_06;
######    SELECT count(*) FROM orders_copy_07;
######    SELECT count(*) FROM orders_copy_08;
######    SELECT count(*) FROM orders_processed;


## Export Data from Hadoop to RDBMS

    sqoop export \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table orders_copy_01 \
        --input-fields-terminated-by \\t \
        --export-dir=/user/hive/warehouse/import_all/orders
    
## Export Data from Hadoop to RDBMS - Using JDBC Batch

    sqoop export \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table orders_copy_02 \
        --input-fields-terminated-by \\t \
        --export-dir=/user/hive/warehouse/import_all/orders \
        --batch
    
## Export Data from Hadoop to RDBMS - Using Mutiple Insert

    sqoop export \
        -Dsqoop.export.records.per.statement=10 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table orders_copy_03 \
        --input-fields-terminated-by \\t \
        --export-dir=/user/hive/warehouse/import_all/orders
    
## Export Data from Hadoop to RDBMS - Controlling No Of Statements Per Transaction

    sqoop export \
        -Dsqoop.export.statements.per.transaction=10 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --input-fields-terminated-by \\t \
        --table orders_copy_04 \
        --export-dir=/user/hive/warehouse/import_all/orders
    
## Exporting with All-or-Nothing Semantics using Staging Table

    sqoop export \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table orders_copy_05 \
        --staging-table orders_staging \
        --clear-staging-table \
        --input-fields-terminated-by \\t \
        --export-dir=/user/hive/warehouse/import_all/orders
    
## Updating an Existing DataSet

    sqoop export \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table orders_copy_06 \
        --input-fields-terminated-by \\t \
        --export-dir=/user/hive/warehouse/import_all/orders \
        --update-key order_id,order_date,order_customer_id,order_status
    
## Updating/Inserting Existing/New DataSet

    sqoop export \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table orders_copy_07 \
        --input-fields-terminated-by \\t \
        --export-dir=/user/hive/warehouse/import_all/orders \
        --update-key order_id,order_date,order_customer_id,order_status \
        --update-mode allowinsert
    
## Handling NULL Values From HDFS
    
    sqoop export \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table orders_copy_08 \
        --input-fields-terminated-by \\t \
        --export-dir=/user/hive/warehouse/import_all/orders \
        --input-null-string '\\N' \
        --input-null-non-string '\\N'
    
## Exporting into a Subset of Columns
    
    sqoop export \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table orders_processed \
        --input-fields-terminated-by \\t \
        --export-dir=/user/hive/warehouse/import_all/orders_processed \
        --columns order_id,order_date
    