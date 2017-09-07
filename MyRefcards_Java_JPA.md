# Javax Persistence annotations


Annotation								|	Applied to	|	Description
----------------------------------------|---------------|--------------------------
@Entity									|	Class		|	Specifies that the class is an entity
@Table									|	Class		|	
@Access									|	Class		|	
@Id										|	Field		|	
@Column									|	Field		|	
@GeneratedValue							|	Field		|	<ul><li>Applied to a primary key property or field of an entity</li><li>@GeneratedValue( strategy = GenerationType.IDENTITY )</li><li>@GeneratedValue( strategy = GenerationType.SEQUENCE, generator = "appUsersSeq" ) @SequenceGenerator( name = "appUsersSeq", sequenceName = "APP_USERS_SEQ", allocationSize = 1, initialValue = 1 )</li><li>@GeneratedValue( strategy = GenerationType.TABLE, generator = "appSeqStore" ) @TableGenerator( name = "appSeqStore", table = "APP_SEQ_STORE", pkColumnName = "APP_SEQ_NAME", pkColumnValue = "APP_USERS.APP_USERS_PK", valueColumnName = "APP_SEQ_VALUE", initialValue = 1, allocationSize = 1 )</li></ul>
@SequenceGenerator						|	Class/Field	|	Defines a primary key generator which will be referenced by @GeneratedValue
@Basic									|	Field		|	

