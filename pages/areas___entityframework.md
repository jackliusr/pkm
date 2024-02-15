- Handling Entity Framework Core database migrations in production
	- part 1
	  collapsed:: true
		- ![](https://www.thereformedprogrammer.net/wp-content/uploads/2019/01/FiveTypesOfMigrations-simple.png){:height 264, :width 567}
		- five ways to create a migration in EF Core
			- [Use EF Core to create a migration](https://www.thereformedprogrammer.net/handling-entity-framework-core-database-migrations-in-production-part-1/#1a-standard-ef-core-c-migration-script) – easy, but doesn’t handle all possible migrations.
			- [Use EF Core to create a migration and then hand-modify the migration](https://www.thereformedprogrammer.net/handling-entity-framework-core-database-migrations-in-production-part-1/#1b-hand-modified-ef-core-c-migration-script) – medium to hard, but handles all possible migrations.
			- [Use a third-partly migration builder](https://www.thereformedprogrammer.net/handling-entity-framework-core-database-migrations-in-production-part-1/#1c-use-a-third-partly-c-migration-builder) to write a C# migration – hard, as you need to write the migration yourself, but you don’t need to know SQL.
			- [Use a SQL database comparison tool](https://www.thereformedprogrammer.net/handling-entity-framework-core-database-migrations-in-production-part-1/#2a-use-sql-database-comparison-tool) to compare databases and output a SQL changes script – easy, but you do need some understanding of SQL.
			- [Write your own SQL migration scripts by copying EF Core’s SQL](https://www.thereformedprogrammer.net/handling-entity-framework-core-database-migrations-in-production-part-1/#2b-hand-coding-sql-migration-scripts) – hard-ish, gives great control but you do need to understand SQL.
		- How to be sure your migration is valid – use **CompareEfSql** tool
	- part 2
		- ![](https://www.thereformedprogrammer.net/wp-content/uploads/2019/01/SixFormsOfDeployment-header.png)
		- file steps
		  ![](https://www.thereformedprogrammer.net/wp-content/uploads/2019/01/FiveStageAppUpdate.png){:height 541, :width 598}
	- Remember that production migrations should be handled with caution to avoid data loss or inconsistencies. It's also a good idea to have a solid backup and recovery strategy in place for your production database, and to thoroughly test migrations in a staging or testing environment before applying them to the live production database.