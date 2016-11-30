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

## Relational Operations

### foreach

	categories = load '/user/hive/warehouse/import_all/categories' as (category_id, category_department_id, category_name);
	categories_id_name = foreach categories generate category_id, category_name;
	dump categories_id_name;

#### Expressions in foreach

	order_items = load '/user/hive/warehouse/import_all/order_items' as (order_item_id, order_item_order_id, order_item_product_id, order_item_quantity, order_item_subtotal, order_item_product_price);
	order_items_promotion_1 = foreach order_items generate order_item_product_id, order_item_quantity + 1;
	order_items_promotion_2 = foreach order_items generate order_item_product_id, $3 + 2;
	dump order_items_promotion_1;
	dump order_items_promotion_2;

#### Projection in foreach

	order_items = load '/user/hive/warehouse/import_all/order_items' as (order_item_id, order_item_order_id, order_item_product_id, order_item_quantity, order_item_subtotal, order_item_product_price);
	beginning = foreach order_items generate ..order_item_product_id; -- produces order_item_id, order_item_order_id, order_item_product_id
	middle    = foreach order_items generate order_item_order_id..order_item_quantity; -- produces order_item_order_id, order_item_product_id, order_item_quantity
	end       = foreach order_items generate order_item_quantity..; -- produces order_item_quantity, order_item_subtotal, order_item_product_price
	dump beginning;
	dump middle;
	dump end;

#### UDFs in foreach

	categories = load '/user/hive/warehouse/import_all/categories' as (category_id, category_department_id, category_name);
	categories_name = foreach categories generate category_department_id, UPPER(category_name) as category_name;
	categories_dept = group categories_name by category_department_id;
	dump categories_dept;
	
#### CASE expressions

	processed = FOREACH loaded GENERATE (
	  CASE i
	       WHEN 0 THEN 'one'
	       WHEN 1 THEN 'two'
	       ELSE 'three'
	  END
	);
	
	processed = FOREACH loaded GENERATE (
	  CASE UPPER(gender)
	       WHEN UPPER('m') THEN 1
	       WHEN UPPER('f') THEN 2
	  END
	) as gendercode;
	
### filter

	categories = load '/user/hive/warehouse/import_all/categories' as (category_id, category_department_id, category_name);
	categories_filtered = filter categories by category_department_id in (1,2,3,4,5);
	dump categories_filtered;
	
	categories_filtered = filter categories by category_name matches 'A.*';
	dump categories_filtered;

	categories_filtered = filter categories_filtered by not category_name matches 'As.*';
	dump categories_filtered;

	categories_filtered = filter categories by category_id  == 2 or category_id  == 20;
	dump categories_filtered;

### group

	-- groups records with the same key
	categories = load '/user/hive/warehouse/import_all/categories' as (category_id, category_department_id, category_name);
	categories_name = foreach categories generate category_department_id, UPPER(category_name) as category_name;
	-- groups records with the same category_department_id
	categories_dept = group categories_name by category_department_id;
	categories_count_by_dept = foreach categories_dept generate group, COUNT(categories_name);
	dump categories_count_by_dept;

	-- group on multiple keys
	customers = load '/user/hive/warehouse/import_all/customers' as (customer_id, customer_fname, customer_lname, customer_email, customer_password, customer_street, customer_city, customer_state, customer_zipcode);
	customers_by_state_zip = group customers by (customer_state, customer_zipcode);
	dump customers_by_state_zip;
	describe customers_by_state_zip;
	customers_count_by_state_zip = foreach customers_by_state_zip generate group, COUNT(customers.customer_id);
	dump customers_count_by_state_zip;
	
### order by

	categories = load '/user/hive/warehouse/import_all/categories' as (category_id, category_department_id, category_name);
	order_by_name = order categories by category_name;
	dump order_by_name;
	
	order_by_deptAndName = order categories by category_department_id, category_name;
	dump order_by_deptAndName;

	order_by_deptDescAndNameAsc = order categories by category_department_id desc, category_name;
	dump order_by_deptDescAndNameAsc;

### distinct

	-- create sample file
	sh echo "1,One" >> /home/cloudera/distinctSample.dat
	sh echo "2,Two" >> /home/cloudera/distinctSample.dat
	sh echo "2,Two" >> /home/cloudera/distinctSample.dat
	sh echo "3,Three" >> /home/cloudera/distinctSample.dat
	sh echo "3,Three" >> /home/cloudera/distinctSample.dat
	sh echo "3,Three" >> /home/cloudera/distinctSample.dat
	sh cat /home/cloudera/distinctSample.dat

	- push it to hdfs
	fs -put distinctSample.dat /user/cloudera/distinctSample.dat
	fs -ls /user/cloudera/distinctSample.dat
	
	-- pig distinct demo
	numbers = load '/user/cloudera/distinctSample.dat' using PigStorage(',') as (num, description); 
	dump numbers;
	distinctNumbers = distinct numbers;
	dump distinctNumbers;

### join

	categories = load '/user/hive/warehouse/import_all/categories' as (category_id, category_department_id, category_name);
	departments = load '/user/hive/warehouse/import_all/departments' as (department_id, department_name);
	join_dept_catg = join departments by department_id, categories by category_department_id;
	describe categories;	
	describe departments;	
	describe join_dept_catg;	
	dump join_dept_catg;
	join_dept_catg_ordered = order join_dept_catg by department_id, department_name, category_id; 
	dump join_dept_catg_ordered;
	describe join_dept_catg_ordered;
	join_dept_catg_ordered_projected = foreach join_dept_catg_ordered generate department_id, department_name, category_id, category_name;
	dump join_dept_catg_ordered_projected;
	
### join types
	
	1. Fragment Replicated Join
		* Large Dataset Joined to Small Dataset
		* Small Dataset loaded into memory
		* Large Dataset will be streamed
		* Supports Inner and Left Outer Joins
	2. Skew Join
		* Suitable for Dataset where few keys have more magnitude of records than other keys
		* Can be Inner or Outer Joins
	3. Sort-Merge Join
		* To Join with already sorted Datasets
	


### limit

	categories = load '/user/hive/warehouse/import_all/categories' as (category_id:long, category_department_id:long, category_name:chararray);
	dump categories;
	categories_first10 = order categories by category_id;
	dump categories_first10;
	categories_first10 = limit categories_first10 10;
	dump categories_first10;

## PigLatin Functions
	SUM()
	TOKENIZE()
	flatten()
	COUNT()
	COUNT_STAR()
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
