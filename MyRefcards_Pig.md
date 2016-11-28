# Pig

## References

###### 1. [Pig Documentation](http://pig.apache.org/docs/r0.16.0/)
###### 2. [Programming Pig by Alan Gates and Daniel Dai (O’Reilly).    Copyright 2017 Alan Gates and Daniel Dai, 978-1-491-93709-9.](https://www.amazon.com/Programming-Pig-Dataflow-Scripting-Hadoop/dp/1491937092)

## Configuring Pig on Your Hadoop Cluster
	
	JAVA_HOME=
	HADOOP_HOME=
	HADOOP_CONF_DIR=$HADOOP_HOME/conf for Hadoop 1 
	HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop for Hadoop 2
	PIG_CLASSPATH=$HADOOP_CONF_DIR

## Data Types

1. Scalar Types
	* int			e.g., as (a:int)
	* long			e.g., as (a:long)
	* biginteger	e.g., as (a:biginteger)
	* float			e.g., as (a:float)
	* double		e.g., as (a:double)
	* bigdecimal	e.g., as (a:bigdecimal)
	* chararray		e.g., as (a:chararray)
	* boolean		e.g., as (a:boolean)
	* datetime		e.g., as (a:datetime)
	* bytearray		e.g., as (a:bytearray)
2. Complex Types
	* MAP			e.g., as (a:map[], b:map[int])
	* TUPLE			e.g., as (a:tuple(), b:tuple(x:int, y:int))
	* BAG			e.g., as (a:bag{}, b:bag{t:(x:int, y:int)})
	
## How to load data

	-- load the categories file
	categories = load '/user/hive/warehouse/import_all/categories';
	
	-- load the tab delimited, categories file using the default PigStorage()
	categories = load '/user/hive/warehouse/import_all/categories' using PigStorage();

	-- load the comma delimited, categories file using the default PigStorage()
	categories = load '/user/hive/warehouse/import_all/categories' using PigStorage(',');
	
	-- load data from HBase
	categories = load '/user/hive/warehouse/import_all/categories' using HBaseStorage();
	
	-- load the categories file with specified schema
	categories = load '/user/hive/warehouse/import_all/categories' as (category_id, category_department_id, category_name);
	
## How to store data

	-- store the processed data into file using default PigStorage() function
	store processed into '/data/examples/processed';

	-- store the processed data as comma delimited file
	store processed into 'processed' using PigStorage(',');
	
	-- store the processed data into file using HBaseStorage() function
	store processed into '/data/examples/processed' using HBaseStorage();

## How to display the output in screen

	dump processed;

## PigLatin Semantics
	describe
	load
	group
	foreach
	generate group
	join
	dump
	filter
	group
	order
	limit
	store

## PigLatin Functions
	SUM()
	TOKENIZE()
	flatten()
	COUNT()
	AVG()
	SUBSTRING()
	UPPER()

## Cloudera Samples

categories
customers
departments
order_items
orders
products

categories = load '/user/hive/warehouse/import_all/categories' as (category_id, category_department_id, category_name);
customers = load '/user/hive/warehouse/import_all/customers' as (customer_id, customer_fname, customer_lname, customer_email, customer_password, customer_street, customer_city, customer_state, customer_zipcode);
departments = load '/user/hive/warehouse/import_all/departments' as (department_id, department_name);
order_items = load '/user/hive/warehouse/import_all/order_items' as (order_item_id, order_item_order_id, order_item_product_id, order_item_quantity, order_item_subtotal, order_item_product_price);
orders = load '/user/hive/warehouse/import_all/orders' as (order_id, order_date, order_customer_id, order_status);
products = load '/user/hive/warehouse/import_all/products' as (product_id, product_category_id, product_name, product_description, product_price, product_image);

dump categories;
dump customers;
dump departments;
dump order_items;
dump orders;
dump products;


categories_filtered_by_id = filter categories by category_id >= 10 and category_id <= 15;
customers_filtered_by_id = filter customers by customer_id >= 10 and customer_id <= 15;
departments_filtered_by_id = filter departments by department_id >= 5;
orders_items_filtered_by_id = filter order_items by order_item_id >= 10 and order_item_id <= 15;
orders_filtered_by_id = filter orders by order_id >= 10 and order_id <= 15;
products_filtered_by_id = filter products by product_id >= 10 and product_id <= 15;

dump categories_filtered_by_id;
dump customers_filtered_by_id;
dump departments_filtered_by_id;
dump orders_items_filtered_by_id;
dump orders_filtered_by_id;
dump products_filtered_by_id;
