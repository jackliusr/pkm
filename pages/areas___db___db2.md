- ```sql
  CREATE DATABASE dbname USING CODESET codeset 
         TERRITORY territory COLLATE USING collation
  ```
	- **Code page** shows the IBM-defined code page as mapped from the operating system code set.
	- **Group** shows whether a code page is single byte ("S"), double-byte ("D"), or neutral ("N"). The "-n" is a number used to create a letter-number combination. Matching combinations show where connection and conversion is allowed by Db2® database systems. For example, all "S-1" groups can work together. However, if the group is neutral, then connection and conversion with any other code page **DB2CODEPAGE**listed is allowed. Graphic strings are not supported where the group indicates that the code page is single byte.
	- **Code set** shows the code set associated with the supported language. The code set is mapped to the Db2 code page.
	- **Territory code** shows the code that is used by the database manager internally to provide region-specific support.
	- **Collation** shows the default collation for non-Unicode databases.
	- **Locale** shows the locale values supported by the database manager.
- ``` bash
  db2 get db cfg for <db name>
  ```
- [DB2CODEPAGE](https://www.ibm.com/docs/en/db2/11.5?topic=support-derivation-code-page-values): windows registry variable
- db2look: Extracts the Data Definition Language (DDL) statements to reproduce the database objects of a production database on a test database.
- [catalog views](https://www.ibm.com/docs/en/SSEPGG_9.7.0/com.ibm.db2.luw.sql.ref.doc/doc/r0011297.html): syscat
- sequence: 
  
  ``` sql
  -- CURRVAL or NEXTVAL 
  select a.nextval 
  
  ```
- backup
	- snapshot backup: A snapshot backup operation uses the fast copying technology of a storage device to perform the data copying portion of the backup.
	  
	  ``` sql
	  --option 1
	  db2 backup db sample use snapshot;
	  --option 2 ADMIN_CMD procedure
	  CALL SYSPROC.ADMIN_CMD
	     ('backup db sample use snapshot')
	  ```