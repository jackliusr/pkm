- description: **SMS Gateway - integration with Dynamics 365**
- William: uportal, call, need to know internal projects to make better decisions
- link: https://dev.azure.com/sntuc/TA%20Board/_workitems/edit/5427/
- **[CR_CR2023-007- SMS Integration](https://sntuc.sharepoint.com/:w:/r/sites/VendorSite/DXC/CR%20-%20Committed%20InProgress/CR2023-007-%20SMS%20Integration%20in%20Marketing/CR%20Paper/CR_CR2023-007-%20SMS%20Integration.docx?d=w88385039020e4dcdbccec46651bdd5dd&csf=1&web=1&e=hQgH8s)**
	- Send Mode:
		- Pre-Blast Verification: every 5 mins
		- Blast Mode:
- https://learn.microsoft.com/en-gb/dynamics365/marketing/real-time-marketing-compliance-settings
- database preparation: A, B, C can be name, phone, first name, last name ?
   ![image.png](../assets/image_1687958656598_0.png){:height 558, :width 372}
- [Requirements_CR2023-038-CRM Online_Setup Up Insight_v1.0](https://sntuc.sharepoint.com/sites/TODataandTechnology/Shared%20Documents/Digital%20Marketing%20Platform/PR%20and%20PO/CR2023-038-Real%20Time%20Marketing/Requirements_CR2023-038-CRM%20Online_Setup%20Up%20Insight_v1.0.docx?web=1)
	- phase 2 main references:
		- [Get started with Dynamics 365 Customer Insights - Data](https://learn.microsoft.com/en-us/dynamics365/customer-insights/data/get-started)
		- [Move from outbound marketing to Customer Insights - Journeys](https://learn.microsoft.com/en-us/dynamics365/customer-insights/journeys/real-time-marketing-move)
	- licenses ? for parallel run or the two apps are separately licensed
	- Dynamics 365 Customer Insights and Dynamics 365 Marketing apps into a single offering. the new Customer Insights offering is expanded to include both the Customer Insights – Journeys (formerly Dynamics 365 Marketing) and Customer Insights – Data (formerly the standalone Customer Insights) applications.
	  ![](https://learn.microsoft.com/en-us/dynamics365/customer-insights/journeys/media/ci-faq-sku-name-change.png){:height 304, :width 696}
	- Dynamics 365 Marketing --> ***Customer Insights – Journeys***
	- Dynamics 365 Customer Insights --> ***Customer Insights – Data***
	- Customer Insights - Journeys enables you to deeply personalize your customer engagement using transactional, behavioral, and demographic data from [Dynamics 365 Customer Insights - Data](https://learn.microsoft.com/en-us/dynamics365/customer-insights).
	- ![Transitioning from Outbound to Real-time Marketing Playbook-7-24-23.pdf](../assets/Transitioning_from_Outbound_to_Real-time_Marketing_Playbook-7-24-23_1695658555658_0.pdf)
	- https://learn.microsoft.com/en-us/shows/dynamics-365-fasttrack-architecture-insights/dynamics-365-marketing-obm-to-rtm-transition-playbook
	- https://aka.ms/OutboundtoRealtimeMarketingPlaybook
	- [Availability](https://learn.microsoft.com/en-us/dynamics365/customer-insights/journeys/ci-faq#availability): Singapore? run us and serve singapore
	- questions?:
		- data first ? outbound marketing will be replaced by real-time?
	- capacity units:
		- **People Interacted** (equivalent to the previous "marketable contact" unit in Dynamics 365 Marketing) that powers the use of **Customer Insights – Journeys**.
		- **People Unified** (equivalent to the previous "profile" meter in Dynamics 365 Customers Insights) which powers **Customer Insights – Data**
	- Re: SMS Gateway - integration with Dynamics 365
		- The new API consists of 2 docs:
		  1. to generate token
		  2. for sending SMS based on the token generated from step
		- ==========================
		- @Jack Liu
		- For the Delivery Receipt API, kindly refer to the 
		  Moobicast-DR-API.pdf