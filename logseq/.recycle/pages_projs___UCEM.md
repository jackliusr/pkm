- UCEM: Unified Customer Experience Management
- UCEM Master Config
- **UCEM Batch entity**
- UCEM architecture
- DB
	- prod, readonly 10.25.15.68
	- uat: via jumphost
- frequently used queries
  
  ``` sql
  select * from ava_masterconfig am where ava_name like '%DBS%'
  ```
- mapping between biz concepts and tables
  |concept | table|
  | -- | --|
  |Company | Account |
  |member | Contact |
  | union | ava_union |
  |union branch | ava_unionbranches|
- configuration tables
  |table_name|row_cnt| usage |
  |----------|-------|-----|
  |ava_masterconfigBase|185|
  |ava_batchconfigurationBase|50|
  |ava_financeconfigurationBase|45| configuration : kv |
  |ava_paymentconfigurationBase|13| month, UASSOCIATE|
  |ava_feeconfigBase|6|membership fee config |
  |dxc_exchangeidsequenceconfigurationBase|4|
  |dxc_occupationgroupconfigBase|3|
  |IsvConfigBase|1|
  |ava_paymentinstruction| | member payment instructions |
- batchconfig
  |ava_category|ava_FileType|ava_membershipType|ava_xmlvalue|
  |---|---|---|---|
  |32|NULL|NULL||
- Process on demand job:
	- schedule: 7am,
	- ConsoleOption: 8
	- ProcessOnDemandFinanceBatch
	- table: ava_financebatch and ava_batch
- SSIS jobs: https://sntuc.sharepoint.com/sites/VendorSite/DXC/Forms/AllItems.aspx?RootFolder=%2Fsites%2FVendorSite%2FDXC%2FAMS%2DCRM%20Incidents%2FNTUC%20Case%20ID%2023823243%20%2D%20Request%20for%20help%20to%20provide%20some%20info%20%2D%20Acknowledged%20INC27768969%2FSSIS%20Batch%20job%20document
- ava_errorlog
- Renci.SshNet.Sftp & SLIFT
- duplicate company code issue