- PM: Huey Eng Hor, Chow Ying Yi, Soh Jing Chang, Brian Fu Ruming
- [Project - 2023 - e-Services & UTAP Replatform](https://sntuc.sharepoint.com/:f:/r/sites/TO-Technology/Shared%20Documents/Project%20-%202023%20-%20e-Services%20%26%20UTAP%20Replatform?csf=1&web=1&e=ZprpFK)
- [TO Waiver Paper For Implement UTAP On A New Independent System.pdf](https://sntuc.sharepoint.com/:b:/r/sites/itd/ItdOnly/Tender%20%20ITQ%20Document/2022%20-%20Replatform%20eService%20and%20UTAP%20applications/UTAP/WOC/TO%20Waiver%20Paper%20For%20Implement%20UTAP%20On%20A%20New%20Independent%20System.pdf?csf=1&web=1&e=ELco0E)
	- estimated $850,957.38, budget $946,000
	- application enhancement/development services by CR man-day rate
	- professional manpower rate
- functionality: whatever is current will have to be replatform as it is. This is what is agreed with e2i. really?
- [UAT, Development, Prod Environment Setup](https://sntuc.sharepoint.com/:f:/r/sites/TO-Technology/Shared%20Documents/Project%20-%202023%20-%20e-Services%20%26%20UTAP%20Replatform/UAT%20and%20Development%20Environment%20Setup?csf=1&web=1&e=hSeI6J)
- env
	- SIT: Email: UTAP SIT - Link and account for testing
	  |URL	|Username	|Password	|Role|
	  | https://utap.ntuceservices.org/Courses/ |usere2il1@gmail.com | Th@nh561986AB | E2I L1 |
	  ||	userse2il2@gmail.com| | E2I L2|
	  ||		usere2il3@gmail.com || E2I L3|
	  ||		pda01111999@gmail.com || TP|
	  ||		phamkhacquydev@gmail.com ||FND officer|
	  ||		baotoannbt96@gmail.com || FND|
	  |https://utap.ntuceservices.org/unionMember| Linkpass: myntuc.uat+891@gmail.com  | mpuat2023	 | |
- | **Environment** | **Server** | **Shared folder** | **User ID** | **Password** |
  | UAT | 10.25.15.69 |     | S-utap-UAT@ntuc.sg | P@ssw0rd! |
  | PROD | 10.25.12.134 |  | S-utap-Prod | ZuB<)gj#K24 |
- table questions:
	- T_RELATIONSHIP
	- T_UTAP_SF_APPLICATION
	- T_PRODUCT
	- T_PROGRAM_INST
- checklist:
  + [ ] a method endpoint to  get the list of URLs of all eServices. in access management
       email keyword: This is to allow application like UMatrix to generate the menu links dynamically.
  + [ ] blacklisted
  + [ ] utap lite
  + [ ] google/bing search result page
- DOING deployment diagram
  :LOGBOOK:
  CLOCK: [2023-04-12 Wed 09:13:29]--[2023-04-12 Wed 10:18:37] =>  01:05:08
  CLOCK: [2023-04-18 Tue 16:34:08]
  :END:
- TODO  TP first time login, prompt hp; check security question mfa with andy
- journey: https://www.figma.com/file/2gBOYNN3c8c1Vgd7GSLQEn/UTAP-Journey-Overview?type=whiteboard&node-id=371-1342&t=O7elYzJ2iJ5EHEaf-0
- users: union members, Finance user, **e2i admin(80%)**, Training provider(organization)
- rules
	- scheme/ rule engines: drools
	- rules: 
	  ``` bash
	  cd /mnt/c/prjs/DXC-NTUC-UPORTAL/UP2/src/sg/ntuc/crms/utap/rules
	  ls -1 *.drl | wc -l 
	  # 95
	  ls -l *.bpmn | wc -l
	  #66
	  ```
- apis: 
  {:height 484, :width 554}
- PII
	- T_UTAP_SF_APPLICATION, column APPLICANT_UIN
	- T_BATCH_AUDIT, column TX_BATCH_DATA
	- T_ENTITY, column ID_ENTITY
	- T_INDIVIDUAL_DTL, column ID_ENTITY_NRIC_FIN
- batch jobs:
	- UtapApplicationStatus
	- UtapClaimApproval
	- UTAPMail:
	- UtapOTCCashDisbReport
	- UtapSAPInboundReport
	- UtapUpdateAppAddressReport
	- UtapUpdateExpiredCourseStatus
- servers:
	- _Migration VM: 10.25.12.49
	- _Jumphost: 10.101.253.36, 10.101.253.37
	- **_Deployment VM: 10.101.250.8**
- NOTICE:
	- font: Roboto font --> **Open Sans**
	- Google Analytics: GA4
	  id:: 64a640a8-6ef3-41a6-b972-b6de72b7de1d
	- convert the time from UTC to SGT time
	- include an API for eService Access to generate the list of URLs for all eServices
- WebEnv
	- UAT:
		- https://uatportal.ntuc.org.sg/wps/portal/up2/home/eserviceslanding
		- [test_admin@test.com](mailto:test_admin@test.com)
		- PAss@ddd22
	- dev:
		- domain: utap.ntuceservices.org
- sites:
	- https://skillsupgrade.ntuc.org.sg/wps/portal/skillsupgrade/home: Member file 
	  application & claim
	- https://www.ntuc.org.sg/wps/portal/up2/home/eserviceslanding
- domain knowledge
	- Users function
	- main biz flow:
	  {:height 499, :width 1021}
	- DONE check value not in ascii values?
	- DONE tables: ERD for those tables ?
		- T_APPLICATION
		- T_Audit_Rule
		- T_AUDIT_RULE_APPROVAL
		- T_DISBURSEMENT
		- T_FUND_RULE
		- T_NOTIFICATION_MANAGE
		- T_TRAININGGRANT_DETAIL
		- T_UTAP_BATCH
		- T_UTAP_DOCUMENT_ACCESS
		- T_UTAP_FILES
		- T_UTAP_MAIL
		- T_UTAP_REJECTION_REASON
		- T_UTAP_SF_APPLICATION
	- references
		- video: [eservice UTAP KT session-20230303_110710-Meeting Recording.mp4 (sharepoint.com)](https://sntuc.sharepoint.com/sites/TO-Technology/_layouts/15/stream.aspx?id=%2Fsites%2FTO%2DTechnology%2FShared%20Documents%2FProject%20%2D%202023%20%2D%20e%2DServices%20%26%20UTAP%20Replatform%2FMeeting%20Recordings%2FUTAP%2Feservice%20UTAP%20KT%20session%2D20230303%5F110710%2DMeeting%20Recording%2Emp4&referrer=Teams%2ETEAMS%2DELECTRON&referrerScenario=p2p%5Fns%2Dbim)
		- programme info: [NTUC | Every Worker Matters](https://unions.ntuc.org.sg/wps/portal/up2/home/aboutntuc/whatwedo/programmes)
		- What's UTAP: https://www.ntuc.org.sg/wps/wcm/connect/9c4d4d804c737af8984ad9074f891cc1/What+is+U-Tap.docx?MOD=AJPERES
		- UTAP_Overview excel file:  https://sntuc.sharepoint.com/:x:/r/sites/TODataandTechnology/_layouts/15/Doc.aspx?sourcedoc=%7B15B19E55-3EC1-444C-8D8A-316ADEF30195%7D&file=UTAP_Overview.xlsx&action=default&mobileredirect=true
		- User Guides
			- [UTAP_TP_User_Guides_For_CR2021_010_v1.1.pptx](https://sntuc.sharepoint.com/:p:/r/sites/VendorSite/DXC/CR%20-%20Committed%20Completed/2021/CR2021-010-UTAP%20Enhancement/CR%20Paper/User%20Guide/UTAP_TP_User_Guides_For_CR2021_010_v1.1.pptx?d=wbf76cad49b39429da6f83950f03e33e7&csf=1&web=1&e=hYr5sW)
			- [UTAP_E2I_User_Guides_For_CR2021_010_v1.1.pptx](https://sntuc.sharepoint.com/:p:/r/sites/VendorSite/DXC/CR%20-%20Committed%20Completed/2021/CR2021-010-UTAP%20Enhancement/CR%20Paper/User%20Guide/UTAP_E2I_User_Guides_For_CR2021_010_v1.1.pptx?d=w6cbc12220cee4bb296a6eb5d01e5cf89&csf=1&web=1&e=iMX5na)
			- [UTAP_User_Guides_For_CR2021_010_v1.1.pptx](https://sntuc.sharepoint.com/:p:/r/sites/VendorSite/DXC/CR%20-%20Committed%20Completed/2021/CR2021-010-UTAP%20Enhancement/CR%20Paper/User%20Guide/UTAP_User_Guides_For_CR2021_010_v1.1.pptx?d=w597e6befe63a48e78a1d237f59e2c23b&csf=1&web=1&e=NkVlWZ)
- UTAP vs UTAP lite: additional CR to implement UTAP-lite for YD Starter Membership, still under UTAP
- blacklisted individuals: is not the membership blacklist but training funding blacklist, now that
  we received MOF funding under NETF. The list of blacklisted individuals are
  based on an excel list provided by SSG/WSG which is updated monthly.
  Blacklisted individuals would not be able to receive any funding even though
  they are union members.
- okta integration for admin only
- SWIFT code: 11 characters; tripple x
- TrainProvider StateChart
  ``` mermaid
  ---
  title: Simple sample
  ---
  stateDiagram-v2
      [*] --> Pending :  creation
      Pending --> Active: FND Director Approval
      Pending --> DRAFT: FND Director reject with reasons
  ```
-
- T_CDMETADATA and T_CDVALUES
- how does UTAP work?
- social login: singpass,linkpass etc. for end users.
- UTAP_TP.xlsx NtuC#1001.
- Eligibility vs Status:
	- It was the original design of the API (inherit from existing logic).Yes, if the status is false, the eligibility will be false too.
- timeline: [Presentation title is Arial Bold 44pt, up to three lines (sharepoint.com)](https://sntuc.sharepoint.com/:x:/r/sites/TO-Technology/_layouts/15/Doc.aspx?sourcedoc=%7B00066C5C-904C-49FF-A7A8-4D29634CD871%7D&file=UTAP%20Timeline.xlsx&action=default&mobileredirect=true)
-