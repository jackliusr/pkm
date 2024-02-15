- SAP Integration Directory: The SAP Integration Directory **manages the objects available in the SAP Integration Repository, along with the particular configuration requirements for a system landscape**. At runtime the information from the SAP Integration Directory is evaluated on the Integration Server.
- license:
	- Full Use Equivalent (FUE): the number that corresponds to the number of individuals authorized to
	  access specified solution capabilities of the RISE with S/4HANA Cloud t Service as follows:
	  1 FUE = 1 SAP S/4HANA for advanced use 1
	  FUE = 5 SAP S/4HANA for core use
	  1 FUE = 30 SAP S/4HANA for self-service use
- Accelerated SAP: ASAP
- BP: business partners
- PI: SAP NetWeaver Process Integration
- SAP NetWeaver Scheduler: ABAP, java
	- business process
- communication channel:  The communication channel is where you configure adapters in particular. Depending on the direction of message processing, you require either a sender or a receiver channel.
- SAP Exchange Infrastructure
- RISE with SAP: a comprehensive solution for driving business innovation together.
- HANA Enterprise Cloud (HEC)
- SAP Business Technology Platform (BTP)
- Cloud Platform Integration (CPI): SAP's cloud-based middleware that integrates cloud and on-premise applications with third-party SAP and non-SAP products.
- Transactions
	- AL11:  displays an overview of all linked SAP directories and their corresponding files. It is used to store data on the application server where SAP and Non-SAP systems can access.
- Ten concepts of interface and integration in SAP-from evolution point of view; a representation of arrival of different techniques in an approximated sequence of chronology.
	- File Interface
	- RPC
	- IDoc
	- SOAP
	- REST
	- S/4 HANA
	- CDS and BOPF
	- Web API
	- Behavior Definition Language (BDL)
- A2A means you are communicating within same firewall or in same company or same land scape.
- Secure Network Communications (SNC)
- SAP HANA MDC: HANA multitenant database containers: eliminate the MCOS – Multiple Components One System (Multiple SAP HANA systems on one SAP HANA) or MCOD – Multiple Components One Database (Multiple schemas on one SAP HANA) scenario that is not supported for Production HANA usage
- Edge Integration Cell: the new flexible hybrid integration runtime, offered as an optional extension to SAP Integration Suite, enabling customers to manage APIs and run their integration scenarios within customer-managed private landscapes.
  collapsed:: true
	- Key Highlights:
		- Flexible deployment option in customer managed private kubernetes environments (Azure AKS, Amazon EKS, SUSE Rancher)
		- Supports use cases of data compliance and governance by processing data locally
		- Design, configure and monitor APIs and integrations in the cloud but run them within your private landscape
		- Configure and manage multiple Edge Integration Cells with an SAP Integration Suite cloud tenant
		- Ensures business continuity during temporary connectivity loss*
		- Offers a migration path for PI/PO customers, to move to SAP Integration Suite, and still be able to run scenarios within their private landscape
	- HLA
	  ![](https://blogs.sap.com/wp-content/uploads/2023/11/architecture.jpg){:height 538, :width 780}
- Cloud Integration
	- [How to Setup Secure Connection to sftp Server](https://blogs.sap.com/2017/08/03/cloud-integration-how-to-setup-secure-connection-to-sftp-server/)
- Collaboration Agreement Objects and Runtime Procedure
  https://help.sap.com/doc/129bd0566c531014b4b8e896e5ddc726/7.0.39/en-US/loioc8be115589227b3ce10000000a174cb4_LowRes.png