- Uportal: migrate from websphere to sitescore umatrix in [[Apr 2023]]. 2 links to eservices and UTAP in umatrix as they are in the progress of migration
- UPortal account, can create, however can't updates
- {:height 484, :width 1050}
- DB:
	- DB2 9.7
	- ``` sql
	  -- get db name
	  select current server,CURRENT_TIMESTAMP,CURRENT_TIMEZONE   from sysibm.sysdummy1;
	  
	  -- get hostname
	  SELECT HOST_NAME FROM TABLE(SYSPROC.ENV_GET_SYS_INFO()) T
	  ```
	- Env
		- UAT
			- server:  UPTESTDBA3
			- DB: UPDBUT
			- connection info
				- db.url=jdbc:db2://UPTESTDBA3:50000/UPDBUT
				- db.username=UPDBUT
				- db.password=Rajobi57
		- Prod
			- Server: UPPRDDBA3
			- DB:   UPDBPR