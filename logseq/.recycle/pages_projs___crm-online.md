- **CRM Online**: case(customer service) & marketing
- phase:
	- indenpendent app to sent SMS
	  logseq.order-list-type:: number
	- setup dynamics 365 insights
	  logseq.order-list-type:: number
	- sms integration
	  logseq.order-list-type:: number
	- integration with external systems (ex: Athena)
	  logseq.order-list-type:: number
- |**Phase**|**Tentative Timeframe**|**Description** |
  |**Phase 1**| Start Time: September 23. End Time: December 23.|To implement a custom Module that is neither integrated with outbound nor real time journeys and is run independently to send SMS. |
  |**Phase 2**| Discussion/Solution Design: November - December Implementation: February|Setup “Dynamics 365 Insights” and train users to start using real time journeys while parallelly using “Dynamics 365 Marketing”. During this phase, we should decide the transition approach/strategy from “Dynamics 365 Marketing” to “Dynamics 365 Insights”.|
  |**Phase 3**|Discussion/Solution Design: 2 Months after phase 2 completion| Implement SMS integration with “Dynamics 365 Insights” and do the transition from “Dynamics 365 Marketing” to “Dynamics 365 Insights”.|
  |**Phase 4**|Can be combined with Phase 3 upon checking the feasibility.| Integration with external systems (Ex: Athena). Requirements are yet to be given by NTUC. |
- [Requirements_CR2023-038-CRM Online_Setup Up Insight_v1.0.docx](https://sntuc.sharepoint.com/:w:/r/sites/TODataandTechnology/Shared%20Documents/Digital%20Marketing%20Platform/PR%20and%20PO/CR2023-038-Real%20Time%20Marketing/Requirements_CR2023-038-CRM%20Online_Setup%20Up%20Insight_v1.0.docx?d=w5479d85901d743bca24a08e785e62c58&csf=1&web=1&e=ltXuCF)
- [CR_CR2023-007- SMS Integration.docx](https://sntuc.sharepoint.com/:w:/r/sites/VendorSite/DXC/CR%20-%20Committed%20InProgress/CR2023-007-%20SMS%20Integration%20in%20Marketing/CR%20Paper/CR_CR2023-007-%20SMS%20Integration.docx?d=w88385039020e4dcdbccec46651bdd5dd&csf=1&web=1&e=uWmT7b)
	- mavenlab: use our apim keys while calling our APIs in addition to whitelisting their IPs.