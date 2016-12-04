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
	
## Beeline

	beeline -u 'jdbc:hive2://localhost:10000/default' -n root -p xxx -d org.apache.hive.jdbc.HiveDriver -e "select * from sales;"
	beeline -u 'jdbc:hive2://localhost:10000/default' -n cloudera -p cloudera -d org.apache.hive.jdbc.HiveDriver -e "select * from sales;"
	

## Hive cli

