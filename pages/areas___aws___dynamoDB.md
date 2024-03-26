- 3 properteis of access patterns
	- data size
	- data shape
	- data velocity
- table class
	- Standard table class
	- DynamoDB Standard-IA
- not support stored procedures
- NoSQL Workbench
	- facet:  represent an application's different data access patterns for Amazon DynamoDB. Facets can help you visualize your data model when multiple data types are represented by a sort key. Facets give you a way to view a subset of the data in a table, without having to see records that don't meet the constraints of the facet. Facets are considered a visual data modeling tool, and don't exist as a usable construct in DynamoDB, as they are purely an aid to modeling of access patterns.
	- aggregate view in NoSQL Workbench for Amazon DynamoDB represents all the tables in a data model
- concepts:
	- table, items, attributes
	- primary key: partition key, composite key ( partition key + sort key)
	- ((6600f5a5-50d0-4260-9552-47af8e20cfcf))
	- ((6600fe9f-2ae7-48b4-92cc-ab046e00892f))
- global table:
	- a collection of one or more replica tables, all owned by a single AWS account.
	- A *replica table* (or *replica*, for short) is a single DynamoDB table that functions as a part of a global table. Each replica stores the same set of data items. Any given global table can only have one replica table per AWS Regio
- index
	- `secondary index`: a data structure that contains a subset of attributes from a table, along with an alternate key to support `Query` and `Scan` operations; alternate key
		- Local: has the same partition key as the base table, but a different sort key
		- Global: An index with a partition key and a sort key that can be different from those on the base table
		- [[areas/aws/dynamoDB/gsi-vs-lsi]]
	- sparse indexes: For any item in a table, DynamoDB writes a corresponding index entry **only if the index sort key value is present in the item**. If the sort key doesn't appear in every table item, or if the index partition key is not present in the item, the index is said to be *sparse*.
- Service, account, and table quotas in Amazon DynamoDB
	- Secondary indexes
	  id:: 6600f5a5-50d0-4260-9552-47af8e20cfcf
		- a maximum of 5 local secondary indexes; a default quota of 20 global secondary indexes per table; create or delete only one global secondary index per `UpdateTable` operation
		- project a total of up to 100 attributes into all of a table's local and global secondary indexes.
	- Partition keys and sort keys
		- `item collection` is the set of items which have the same value of partition key attribute
		- For a table with one or more LSIs, item collections cannot exceed 10GB in size. This includes all base table items and all projected LSI views which have the same value of the partition key attribute.
	- API-specific limits
- DynamoDB Streams
  id:: 6600fe9f-2ae7-48b4-92cc-ab046e00892f
	- change data capture
	- event as stream record
	  id:: 6600fecb-d405-4f55-9110-ea1e0822fa39
	- an optional feature
- DynamoDB API
	- Working with items and attributes
		- batch operations:
			- `BatchGetItem`: Read up to 100 items from one or more tables.
			- `BatchWriteItem`: Create or delete up to 25 items in one or more tables
		- ReturnValues:
			- ALL_OLD
			- ALL_NEW
			- UPDATED_OLD
			- UPDATED_NEW
	- expressions:
		- Projection expressions: a string that identifies the attributes that you want. For multiple attributes, the names must be comma-separated.
		- *expression attribute name*： a placeholder that you use in an Amazon DynamoDB expression as an alternative to an actual attribute name. An expression attribute name must begin with a pound sign (`#`), and be followed by one or more alphanumeric characters and the underscore (`_`) character
		- Expression attribute values
			- *Expression attribute values* in Amazon DynamoDB are substitutes for the actual values that you want to compare—values that you might not know until runtime. An expression attribute value must begin with a colon (`:`) and be followed by one or more alphanumeric characters
		- [[areas/aws/dynamoDB/functions]]
		- Condition expressions: conditional write
		- update expression：
		  ```bnf
		  update-expression ::=
		      [ SET action [, action] ... ]
		      [ REMOVE action [, action] ...]
		      [ ADD action [, action] ... ]
		      [ DELETE action [, action] ...]
		  ```
	- query
		- *key condition expression*: a string that determines the items to be read from the table or index. You must specify the partition key name and value as an equality condition. You cannot use a non-key attribute in a key condition expression.
		- filter expression: determines which items within the `Query` results should be returned to you.
		- Limiting the number of items in the result set:
- data modeling
	- **single table** vs multiple table
	- building blocks
		- Composite sort key
		- Multi-tenancy
		- Sparse index
		- Time to live
		- Time to live archival
		- Vertical partitioning
		- Write sharding
-