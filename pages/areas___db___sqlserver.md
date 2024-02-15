- Service Master Key: **the root of the SQL Server encryption hierarchy**. The SMK is automatically generated the first time the SQL Server instance is started and is used to encrypt a linked server password, credentials, and the database master key in each database.
- Transactional replication:
	- typically starts with a snapshot of the publication database objects and data. As soon as the initial snapshot is taken, subsequent data changes and schema modifications made at the Publisher are usually delivered to the Subscriber as they occur (in near real time)
	  ![](https://learn.microsoft.com/en-us/sql/relational-databases/replication/transactional/media/trnsact.gif?view=sql-server-ver16){:height 661, :width 329}
	- Publication types
		- Standard transactional publication
		- Transactional publication with updatable subscriptions: two types updatable subscriptions
			- Immediate updating: The Publisher and Subscriber must be connected to update data at the Subscriber.
			- Queued updating: The Publisher and Subscriber do not have to be connected to update data at the Subscriber. Updates can be made while the Subscriber or Publisher is offline.
		- Peer-to-peer topology
		- Bidirectional transactional replication
	- supports updates at Subscribers through updatable subscriptions and peer-to-peer replication