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
	
## Beeline

	beeline -u 'jdbc:hive2://localhost:10000/default' -n root -p xxx -d org.apache.hive.jdbc.HiveDriver -e "select * from sales;"
	beeline -u 'jdbc:hive2://localhost:10000/default' -n cloudera -p cloudera -d org.apache.hive.jdbc.HiveDriver -e "select * from sales;"
	

## Hive cli

