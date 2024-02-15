- [UCEM Batch Job Detail V1.2.docx](https://sntuc.sharepoint.com/:w:/r/sites/VendorSite/DXC/Batch%20Jobs/UCEM%20Batch%20Job%20Detail%20V1.2.docx?d=w88af14f485084f9a8216fe51e42b0172&csf=1&web=1&e=m5ON1V)
- http://ucemuat.ntuc.sg:5555/UCEMUAT2
- ava_masterconfig:
	- SLIFT
		- ```
		  SLIFT_CER	D:\UCEMPRODUCTION\SliftKeys\DBSBANK2026.cer
		  SLIFT_CONSOLE	C:\Program Files (x86)\PrivyLink\SLIFT-Ez Classic\1.4\sliftc.exe
		  SLIFT_PFX	D:\UCEMPRODUCTION\SliftKeys\NTUC_UCEM_Production_2026.pfx
		  SLIFT_PFX_PASSWORD	P@ssw0rd
		  SLIFT_TEMP	D:\UCEMPRODUCTION\SliftTemp
		  SLIFT_CER_WIRECARD	D:\UCEMPRODUCTION\SliftKeys\WDSG_BTP_PROD.cer
		  
		  SAP_SLIFT_CER	D:\UCEMPRODUCTION\SliftKeys\DBSBANK2026.cer
		  SAP_SLIFT_CONSOLE	C:\Program Files (x86)\PrivyLink\SLIFT-Ez Classic\1.4\sliftc.exe
		  SAP_SLIFT_PFX	D:\UCEMPRODUCTION\SliftKeys\NTUC_UCEM_Production_2026.pfx
		  SAP_SLIFT_PFX_PASSWORD	P@ssw0rd
		  SAP_SLIFT_TEMP	D:\UCEMPRODUCTION\SliftTemp
		  ```
	- DBS_XML_IN
		- ``` xml
		  <root>
		   <FileInfo>  
		     <Type>FIXED LENGTH FILE</Type>  
		     <Sftp Host="dsga2sftp-ak.dbs.com" Port="9122" Username="NTUC01" Path="Outbox" 
		           PrivateKeyFile="ooprmuqQBiFthQSVmeIhPJBC9td1EeD0O2b85YnqvtwzK+RxZ1C5Sw==" PassPhrase="HjnlOuW+RuFELj1mbf6S6g=="  
		           SubPath=""  Format="{0}.txt" SLIFT="" SAP="" SubPathMapping=""  RegexMask= '_\w+\d*' />  
		    </FileInfo>
		  </root>
		  ```
	- DBS_XML_OUT
		- ``` xml
		  <?xml version="1.0" encoding="UTF-8"?> <root> 
		    <FileInfo> <Type>FIXED LENGTH FILE</Type> 
		      <Sftp Host="dsga2sftp-ak.dbs.com" Port="9122" Username="NTUC01" Path="Inbox" 
		            PrivateKeyFile="ooprmuqQBiFthQSVmeIhPJBC9td1EeD0O2b85YnqvtwzK+RxZ1C5Sw==" 
		            PassPhrase="HjnlOuW+RuFELj1mbf6S6g==" Format="{0}.txt" RegexMask= ""
		            SLIFT='' SAP='' SubPath="" SubPathMapping="" SAPFiles="ACK1;ACK2;ACK3;MT940" /> 
		    </FileInfo> 
		  </root>
		  ```
- SSIS GIRO
	- [GIRO Deduction File](https://sntuc.sharepoint.com/:w:/r/sites/TODataandTechnology/Shared%20Documents/Project%20Athena%20(UCEM%20Upgrade)/Shared%20with%20NCS/Interfaces/batch%20jobs/SSIS%20Batch%20job%20document/GIRO%20Deduction%20File%20SSIS%20Process%20Flow%20v1.0.1.docx?d=w6af56d138e094816a18babb241c814bd&csf=1&web=1&e=vAGLQ0)
		- |No |	Name	 |Schedule	 |Time	 | Remarks|
		  |1	|SSIS GIRO DEDUCTION FILE TO BANK |	Mon to Fri	|9:00 pm	| Prepare the file(s) Express and APAY|
		  |2	 |H2H SFTP Transfer|	Daily|	4:00 pm|	File created from GIRO Deduction File to Bank will be uploaded to DBS SFTP server. |
		  |3	|SSIS GIRO DEDUCTION RETURN|	Daily|	3:00 am, 8:00 am	| Process return files by DBS |
		  |4	|GIRO DEDUCTION BANK RETURN FILE|	Daily |	6:30 am, 6:30 pm|	Get the return files and create finance batch header (GIRO Return File). |
- Run On Demand Finace Batch
	- batchfile: PROCESS ON DEMAND JOB.BAT
	- 2015-11-01T00:45:00, daily
	- ava_financebatch and ava_batch
	- ava_category in { 20, 10, 11 }
- Fair Price Rebates Yearly
	- batch file: FAIRPRICE_REBATES_(YEARLY).BAT
	- ConsoleOption: 17, however it is used by "Create Instant Card File To LINK"
	  background-color:: red
	- ava_category : 15
- Create Instant Card File To LINK
- FAIREPRICE REBATE SETUP:
	- [UCEM doc:](https://sntuc.sharepoint.com/:w:/r/sites/VendorSite/DXC/Batch%20Jobs/UCEM%20Batch%20Job%20Detail%20V1.2.docx?d=w88af14f485084f9a8216fe51e42b0172&csf=1&web=1&e=G3NbKB&nav=eyJoIjoiMTg3NjM4MTk0MCJ9)
	- batch file: GENERATE_FAIRPRICE_REBATE_SETUP_FILE.BAT
	- ConsoleOption: 18
	- BatchCategory: 13
- FAIRPRICE REBATE TERMINATION
	- ``` bash
	  xx156.xml:46:      <Command>"D:\UCEMPRODUCTION\TerminationReport\Output - Copy.bat"</Command>
	  xx163.xml:41:      <Command>D:\UCEMPRODUCTION\TerminationReport\Output-test.bat</Command>
	  ```
- NFC SFTP Weekly
	- [UCEM Batch Job Detail V1.2.docx](https://sntuc.sharepoint.com/:w:/r/sites/VendorSite/DXC/Batch%20Jobs/UCEM%20Batch%20Job%20Detail%20V1.2.docx?d=w88af14f485084f9a8216fe51e42b0172&csf=1&web=1&e=9GDWMs&nav=eyJoIjoiMTMyNjU2NjkxNiJ9)
	- batch file: NFC SFTP JOB.BAT
	- ConsoleOption: 65
	- Class: BatchProcess_NFCSFTP
- nEBO MEMBERSHIP IMPORT
	- [UCEM Batch Job Detail V1.2.docx](https://sntuc.sharepoint.com/:w:/r/sites/VendorSite/DXC/Batch%20Jobs/UCEM%20Batch%20Job%20Detail%20V1.2.docx?d=w88af14f485084f9a8216fe51e42b0172&csf=1&web=1&e=vTxJKk&nav=eyJoIjoiNDcxNzI4NjQyIn0%3D)
	- batch file: nEBO MEMBERSHIP IMPORT.bat
	- ConsoleOption: 20
	- ava_category: 30
	- class: nEBOMembersCreate
- NTUC Social Membership To UCEM
	- [UCEM Batch Job Detail V1.2.docx](https://sntuc.sharepoint.com/:w:/r/sites/VendorSite/DXC/Batch%20Jobs/UCEM%20Batch%20Job%20Detail%20V1.2.docx?d=w88af14f485084f9a8216fe51e42b0172&csf=1&web=1&e=K1JEVn&nav=eyJoIjoiNDY5NDExMCJ9)
- CCR Deduction File to Bank
	- [UCEM Batch Job Detail V1.2.docx](https://sntuc.sharepoint.com/:w:/r/sites/VendorSite/DXC/Batch%20Jobs/UCEM%20Batch%20Job%20Detail%20V1.2.docx?d=w88af14f485084f9a8216fe51e42b0172&csf=1&web=1&e=Pi4dQC&nav=eyJoIjoiMTU0NDA3MTQ4MyJ9)
	- ConsoleOption: 74
	- Class: WirecardCCRDeduction
- CCR Deduction Bank Return File
	- [UCEM Batch Job Detail V1.2.docx](https://sntuc.sharepoint.com/:w:/r/sites/VendorSite/DXC/Batch%20Jobs/UCEM%20Batch%20Job%20Detail%20V1.2.docx?d=w88af14f485084f9a8216fe51e42b0172&csf=1&web=1&e=Y1GgvH&nav=eyJoIjoiMTM5NzgyNjE5MSJ9)
	- ConsoleOption: 76
	- WirecardCCRDeductionReturn
- H2H File transfer
	- [UCEM Batch Job Detail V1.2.docx](https://sntuc.sharepoint.com/:w:/r/sites/VendorSite/DXC/Batch%20Jobs/UCEM%20Batch%20Job%20Detail%20V1.2.docx?d=w88af14f485084f9a8216fe51e42b0172&csf=1&web=1&e=E59CTd&nav=eyJoIjoiMTQ0NDk3NTY2NCJ9)
	- ConsoleOption: 21
	- ava_category: 32
- LINK IMPORT REALLOCATED CAN NUMBERS
	- [UCEM Batch Job Detail V1.2.docx](https://sntuc.sharepoint.com/:w:/r/sites/VendorSite/DXC/Batch%20Jobs/UCEM%20Batch%20Job%20Detail%20V1.2.docx?d=w88af14f485084f9a8216fe51e42b0172&csf=1&web=1&e=OGuymS&nav=eyJoIjoiMTEyMjE5NzAyNCJ9)
	- ConsoleOption: 19
	- ava_category: 22
	- ava_batch: 22
		- ``` xml
		  <Sftp Host='sftp8822.ntuc.org.sg' Port='8822' Username='ucemlink1' 
		    Password='525uqT9U5KMWnp4syiXAKQ==' Path='Input/PREISSUE_INCORRECT' />
		  
		  #prod
		  <root>  <FileInfo>  
		     <Sftp Host='sftp8822.ntuc.org.sg' Port='8822' Username='ucemlink1' 
		                            Password='525uqT9U5KMWnp4syiXAKQ=='
		                            Path='Input/PREISSUE' /> 
		    </FileInfo> </root>
		  ```