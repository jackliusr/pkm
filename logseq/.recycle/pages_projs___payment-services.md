- links
	- [NTUC_PS_API_Technical_Specification WIP (APIKEY) v2.3.1.docx](https://sntuc.sharepoint.com/:w:/r/sites/TODataandTechnology/Shared%20Documents/YD%20NTUC%20Starter%20App/Shared%20with%20Palo/Technical/FusionEx/NTUC_PS_API_Technical_Specification%20WIP%20(APIKEY)%20v2.3.1.docx?d=w49f70566afab4b2e9e3aca5108ad77be&csf=1&web=1&e=a7nm8h)
	- [2020 - E-Payment Solution with MPGS_DBS](https://sntuc.sharepoint.com/sites/itd/ItdOnly/Tender%20%20ITQ%20Document/Forms/AllItems.aspx?FolderCTID=0x012000E90FCF063FCBCC4A9B5A05363557F0A6&id=%2Fsites%2Fitd%2FItdOnly%2FTender%20%20ITQ%20Document%2FTender%20in%20Year%202020%2F2020%20%2D%20E%2DPayment%20Solution%20with%20MPGS%5FDBS&viewid=cdecb781%2Dec64%2D4f50%2Daa59%2Df64b1ad0f30b)
	- [NTUC_PS_System_Design_Specification Final v2.3.0.docx.pdf](https://sntuc.sharepoint.com/:b:/r/sites/itd/ItdOnly/Tender%20%20ITQ%20Document/Tender%20in%20Year%202020/2020%20-%20E-Payment%20Solution%20with%20MPGS_DBS/Technical/Fusionex%20Docs/System%20Design%20Specs/NTUC_PS_System_Design_Specification%20Final%20v2.3.0.docx.pdf?csf=1&web=1&e=GEeQcm)
	- [RAPID Technical Parameters_NTUC(Filled by Fusionex V2).xlsx](https://sntuc.sharepoint.com/:x:/r/sites/itd/ItdOnly/Tender%20%20ITQ%20Document/Tender%20in%20Year%202020/2020%20-%20E-Payment%20Solution%20with%20MPGS_DBS/Technical/Fusionex%20Docs/SubmissionOfTechnicalParameters/RAPID%20Technical%20Parameters_NTUC(Filled%20by%20Fusionex%20V2).xlsx?d=w1a08395ebf7e4055a374bd68e84fb7cd&csf=1&web=1&e=DcYFik)
	- [NTUC Payment Service -  Operation Guides v1.1_20210510.docx](https://sntuc.sharepoint.com/:w:/r/sites/itd/ItdOnly/Tender%20%20ITQ%20Document/Tender%20in%20Year%202020/2020%20-%20E-Payment%20Solution%20with%20MPGS_DBS/Technical/Fusionex%20Docs/Operation%20Guide/NTUC%20Payment%20Service%20-%20%20Operation%20Guides%20v1.1_20210510.docx?d=w27cdadf8a5ba4f8787e569ae6daab5eb&csf=1&web=1&e=6eUUUV)
- PM: **Jenny Entan**
- vendor: **fusionex**
- TODO:  the batch request and return files?
	- batch job?
	- CCR DEDUCTION BANK RETURN FILE?
- Pre-Requisite
	- By Business Application
		- appid: Identifier of the business application that currently calling the payment service. UP (represent existing Uportal)
		- encryption key (AES-256):
		- password: Used in the basic authentication header during API call.
		- DDA Reference No: for NTUC Customer DDA Account Set Up
	- By Payment Service
	  |Information | Description |
	  |Client Return Url | A url in business application for payment service to redirect to after processed payment*For mobile application, this value is not required  |
	  |Callback Url | API URL from business application to be used during callback batch as well as during online payment Refer to segment 4 |
- Actor: OneCare, UPortal, MyNTUC
- server: NTUCAUTH
- serviceaccount: ePaySVC01
- OS: Window Server 2016
- env
	- UAT	https://epaymentuat.ntuc.org.sg/NTUCWeb
	- PROD	https://epayment.ntuc.org.sg/NTUCWeb
- UTAP?
- Tech Stack:
	- mysql: user PSAppUser
	- .net
	- app-service
- apps --> payments --> FusionEx -->MBGS/DBS...
- batch application: perform recurring payment processing and also payment callback processing.
- TODO NTUC Payment Service
- flow:
- web app
	- with MPGS
		- one time payment
		- one time payment with recurring (same card)
		- recurring
		- api : v61
		- batch: **v51**
	- with DBS
		- one time payment with paynow
		- one time FAST collection payment and recurring with GIRO
		- recurring payment with GIRO
		  |Payment Method| DBS Service | integration method|
		  |PayNow  | DBS MAX | API |
		  | DDA | Direct Debit Authorization| API |
		  |FAST Collection| FAST Collection *After RDDA Setup for One Time Payment| API|
- batch: server to server,
	- callback batch: Callback batch is a server-to-server communication between  business application and the payment service. This is intended to update the business application on the payment result.
	- recurring batch: To perform recurring payment on MPGS payment gateway.
- api (auth, retrieve order, retrieve batch)
- Batch Application: console app, scheduler by Window Task Scheduler
- UCEM batch job:
	- workflow: NTUCCRMSolution/NTUCUCEM/NTUCUCEM/Workflow/CCRInstructionWF.cs
	- 76: CCR INSTRUCTION FILE
	- 75