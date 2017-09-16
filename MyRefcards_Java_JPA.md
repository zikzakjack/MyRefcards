# JPA

## ORM Impedance MisMatch

Mismatch				|	Explanation	
------------------------|---------------
Granularity MisMatch	|	Object Model is more granular than the Relational Model
Inheritance MisMatch	|	Inheritance hierarchy is in Object Model but not in Relational Model
Identity MisMatch 		|	Object Identity & Equality concepts in Object Model vs Primary Key constraint in Relational Model
Association MisMatch	|	Object References in Object Model vs Foreign Key references in Relational Moadel
Data Navigation			|	Navigate the Object graph vs SQL Joins

## Aggregation & Composition

- Aggregation : When the whole is destroyed, its parts are not destroyed. E.g., When the Band is destroyed, its Artists are not destroyed
- Composition : When the whole is destroyed, its parts are also destroyed. E.g., When the House is destroyed, its Rooms are also destroyed


## JPA Persistence annotations

Annotation								|	Applied to	|	Description
----------------------------------------|---------------|--------------------------
@Entity									|	Class		|	Specifies that the class is an entity
@Table									|	Class		|	
@Access									|	Class		|	
@Id										|	Field		|	
@Column									|	Field		|	
@GeneratedValue							|	Field		|	<ul><li>Applied to a primary key property or field of an entity</li><li>AUTO: Hibernate selects the generation strategy based on the used dialect</li><li>IDENTITY: Hibernate relies on an auto-incremented database column to generate the primary key</li><li>SEQUENCE: Hibernate requests the primary key value from a database sequence</li><li>TABLE: Hibernate uses a database table to simulate a sequence</li></li><li>@GeneratedValue( strategy = GenerationType.IDENTITY )</li><li>@GeneratedValue( strategy = GenerationType.SEQUENCE, generator = "appUsersSeq" ) @SequenceGenerator( name = "appUsersSeq", sequenceName = "APP_USERS_SEQ", allocationSize = 1, initialValue = 1 )</li><li>@GeneratedValue( strategy = GenerationType.TABLE, generator = "appSeqStore" ) @TableGenerator( name = "appSeqStore", table = "APP_SEQ_STORE", pkColumnName = "APP_SEQ_NAME", pkColumnValue = "APP_USERS.APP_USERS_PK", valueColumnName = "APP_SEQ_VALUE", initialValue = 1, allocationSize = 1 )</li></ul>
@SequenceGenerator						|	Class/Field	|	Defines a primary key generator which will be referenced by @GeneratedValue
@Transient								|	Field		|	Specifies that the property or field is not persistent
@Temporal								|	Field		|	<ul><li>Specified for persistent fields or properties of type java.util.Date and java.util.Calendar</li><li>TemporalType.DATE - Map as java.sql.Date</li><li>TemporalType.TIME - Map as java.sql.Time</li><li>TemporalType.TIMESTAMP - Map as java.sql.Timestamp</li></ul>
@Basic									|	Field		|	

