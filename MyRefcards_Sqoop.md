# Sqoop

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
        --warehouse-dir=/user/hive/warehouse \
        --hive-import
    
## Import a Table in SequenceFile format

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --warehouse-dir=/user/hive/warehouse \
        --as-sequencefile
    
## Import a Table in Avro File format

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --warehouse-dir=/user/hive/warehouse \
        --as-avrodatafile
    
## Import a Table in Parquet File format

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --warehouse-dir=/user/hive/warehouse \
        --as-parquetfile
    
## Import a Table in GZip compressed format

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --warehouse-dir=/user/hive/warehouse \
        --compress
    
## Import a Table in BZip2 compressed format

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --warehouse-dir=/user/hive/warehouse \
        --compress    
        --compression-codec org.apache.hadoop.io.compress.BZip2Codec
    
## Import only a sub-set of Table data

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --where "department_id > 10" \
        --warehouse-dir=/user/hive/warehouse \
        --hive-import
    
## Override Column Type Mapping

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --warehouse-dir=/user/hive/warehouse \
        --map-column-java department_id=Long,department_name=String
    
## Override Column Type Mapping

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --warehouse-dir=/user/hive/warehouse \
        --map-column-java department_id=Long,department_name=String
    
## Increasing the Number Of Mappers For Larger Dataset

    sqoop import \
        -m 10 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --warehouse-dir=/user/hive/warehouse \
        --hive-import
    
## Handling NULL Values From Database

    sqoop import \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --table departments  \
        --warehouse-dir=/user/hive/warehouse \
        --null-string '\\N' \
        --null-non-string '\\N'
    
## Bulk Import All Tables

    sqoop import-all-tables \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --warehouse-dir=/user/hive/warehouse \
        --hive-import
    
## Exclude Tables During Bulk Import

    sqoop import-all-tables \
        -m 1 \
        --connect jdbc:mysql://quickstart:3306/retail_db \
        --username=retail_dba \
        --password=cloudera \
        --warehouse-dir=/user/hive/warehouse \
        --exclude-tables orders,customers \
        --hive-import
    
