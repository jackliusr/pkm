- batches:  PLS in Batch 2
  {:height 347, :width 688}
- [Waiver Paper For Re-Platform eServices.pdf](https://sntuc.sharepoint.com/:b:/r/sites/itd/ItdOnly/Tender%20%20ITQ%20Document/2022%20-%20Replatform%20eService%20and%20UTAP%20applications/eServices/WOC/Waiver%20Paper%20For%20Re-Platform%20eServices.pdf?csf=1&web=1&e=rZLicx)
	- estimated $644,412.47, budget: $718,300
	- id:: 64d1a215-a7d4-4bb8-90ff-b3cd7e9a2404
- traffic flow: api gateway; if webpages & assets, goto ASE internal load balancer (ILB). api --> apim ->ASE internal load balancer
- [NTUC eService - jMeter - Guideline - v1.0](https://sntuc.sharepoint.com/sites/TO-Technology/Shared%20Documents/Project%20-%202023%20-%20e-Services%20&%20UTAP%20Replatform/Testing/Performance%20-%20Report/NTUC%20eService%20-%20jMeter%20-%20Guideline%20-%20v1.0.docx?web=1)
- estatement-replatform
- deployment flow
	- Deployment in SIT: we compile build package on local then copy to Deployment VM in DXC SIT for testing. If all issues are fixed, we copy package to Deployment VM in NTUC environment, then deploy to UAT and PATH slot using Kudu dashboard.
		- packake -> deployment VM in DXC SIT -->Deployment VM in NTUC environment -> UAT and Prod slot using kudu dashboard
- PII
	- NRIC field - IndividualDraft, MemberBiodata, MemberCompany
- TODO https://sntuc.sharepoint.com/:p:/r/sites/TO-Technology/_layouts/15/Doc.aspx?sourcedoc=%7B3B723E9A-087E-43F9-BA07-C4922E4D35B6%7D&file=e-Services%20Batch%202%20-%20OB%20Additional%20Payment%20Approach_v0.3.pptx&action=edit&mobileredirect=true
- [NTUC eService - User Guide - Manage Defect on Azure v0.1.docx](https://sntuc.sharepoint.com/:w:/r/sites/TO-Technology/Shared%20Documents/Project%20-%202023%20-%20e-Services%20%26%20UTAP%20Replatform/UTAP%20User%20UAT/NTUC%20eService%20-%20User%20Guide%20-%20Manage%20Defect%20on%20Azure%20v0.1.docx?d=w36edaccf7b8848c7800329397c0053de&csf=1&web=1&e=SCXVCG)
	- ``` mermaid
	  stateDiagram-v2
	      [*] --> Proposed
	      Proposed --> Closed : Rejected
	      Proposed --> Active: Approved
	      Active --> Proposed: Investigation Complete
	      Active --> Verification: Fixed
	      Verification --> Active: Not Fixed
	      Verification --> Closed: Verified
	      Closed --> Active: Closed in Error
	      Closed --> [*]
	  ```