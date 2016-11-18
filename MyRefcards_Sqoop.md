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

## Provide Password from a Password File

    sqoop list-tables \

        --connect jdbc:mysql://quickstart:3306/retail_db \
    
        --username=retail_dba \
    
        --password-file my-sqoop-pwd-file

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
    
## Import a Table in GZip compressed format

    sqoop import \

        -m 1 \
    
        --connect jdbc:mysql://quickstart:3306/retail_db \
    
        --username=retail_dba \
    
        --password=cloudera \
    
        --table departments  \
    
        --warehouse-dir=/user/hive/warehouse \
    
        --compress
    
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
    
    