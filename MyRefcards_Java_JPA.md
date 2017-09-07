# Javax Persistence annotations


Annotation								|	Applied to	|	Description
----------------------------------------|---------------|--------------------------
@Entity									|	Class		|	Specifies that the class is an entity
@Table									|	Class		|	
@Access									|	Class		|	
@Id										|	Field		|	
@Column									|	Field		|	
@GeneratedValue							|	Field		|	<ul><li>Applied to a primary key property or field of an entity</li><li>@GeneratedValue( strategy = GenerationType.IDENTITY )</li><li>@GeneratedValue( strategy = GenerationType.SEQUENCE, generator = "appUsersSeq" ) @SequenceGenerator( name = "appUsersSeq", sequenceName = "APP_USERS_SEQ", allocationSize = 1, initialValue = 1 )</li><li>@GeneratedValue(strategy=TABLE, generator="CUST_GEN")</li></ul>
@SequenceGenerator						|	Field		|	
@Basic									|	Field		|	

