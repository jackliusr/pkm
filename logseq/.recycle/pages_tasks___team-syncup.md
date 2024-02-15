- [task:](https://dev.azure.com/sntuc/TA%20Board/_boards/board/t/TA%20Board%20Team/Subactivity?text=jack&System.AssignedTo=%40me)
	- bank gateway
	- sftp finix connection(target Nov 10, if starhub & fujitsu can't complete, Jenny will escalate the request to highest level in fujitsu") 27.  ( go through internet)
	- public ip services:( wiki page to store info)
	- CA Doc & Power VA (start next week, just tried a link)
	- membership platform AKS upgrades
	- tech stack review for UMatrix
		- (SaaS sitecore. basically it is a CMS, bigbox, version, frontend js)
		- aks version,
		- linkpass, ga
		- upgrade by their own cycle
		- Sitecore upgrade
- meeting 2023-11-10
	- bank gateway: sandbox webjob, no way to support smb due to restrictions of webjob sandbox, have to use sftp, blob
	  ``` 
	  Regardless of address, applications cannot connect to anywhere using ports 445, 137, 138, and 139. 
	  In other words, even if connecting to a non-private IP address or the address of a virtual network, 
	  connections to ports 445, 137, 138, and 139 are not permitted.
	  
	  
	  The following are all known SMB v2/v3 ports:
	  
	  TCP 445 — SMB over transmission control protocol (TCP) without the need for a network basic input/output system (NetBIOS).
	  UDP 137 — SMB over user datagram protocol (UDP or Name Services).
	  UDP 138 — SMB over UDP (datagram).
	  TCP 139 — SMB over TCP (session service).
	  ```
	- sftp connectivity issue: starhub already added the IP segments, need to verify from starhub or SAP
	- chat POC:  just cleared my on-hand tasks which will block others. start to work on it next week
	- UTAP replatform:  DXC showed me their migration script, I don't think they can get correct delta data based on their current implementation. I have told them and give them my thoughts on that.
- meeting 2023-11-03
  collapsed:: true
	- bank gateway: IP whitelisting
	- sftp finix connection(target Nov 10, if starhub & fujitsu can't complete, **Jenny will escalate the request to highest level in fujitsu**", if not, itso and dss(funhan, grace, jenny) ), still will be a risk as starhub is circling around without progress
	- shared folder: checking OCBC and final_paymentlistOLD
	- **aks of member-platform:** dev, uat envs aleady were upgraded. however dxc don't work out how to backup and rollback. there is no complete backup and rollback plan. DXC want NTUC do that backup, however DXC don't know if the backup can be used to setup/restore a cluster. ( backup plan: standby, escalation in place)
- meeting 2023-10-25
  collapsed:: true
	- bank gateway:
		- POs for both licenses and CR is out, **UAT in dec/Jan**
	- **sftp FINIX connection:**
	- UTAP:
		- onboarding e2i training providers using **mobile and security questions** as multiple factors, service desk might create accounts  in a manual way. it takes too long
	- public ip services
	  collapsed:: true
		- dpc:
			- report:  202.176.197.150
			- payment: 202.176.197.212, 202.176.197.146
		- azure:
			- ase
				- (zrs): **104.43.52.193, 104.43.50.200**
				- lrs:
			- firewall: **20.205.240.236, 20.24.128.115** (sftp direct)
				- apim -> firewalls
				- payment calls: DBS RAPID system: API calls
				- bank gateway: DBS IDEAL, SFTP
				- sftp: **20.24.128.115**, need 2 IPs
	- notes:
		- YD starter: linux, app service, nodejs, pwa, **stripe**
- meeting 2023-10-18
  collapsed:: true
	- bank gategway
	  
	  ``` 
	  removed sharing, monitoring, move to verication state (add end date)
	  \\UCEMPRDPFT\UA_SFTPBox
	  \\UCEMPRDPFT\DB-BKUP
	  \\UCEMPRDPFT\UP2_Report_Before2017
	  \\UCEMPRDPFT\Report
	  
	  keep  folder as  there are still files deposited from Jul 2023  (the job is turn off). 
	    (SIRS is not used, who deposit files , trace source who, archives, monitor again and do the process, check content of files), 
	    keep active
	  \\UCEMPRDPFT\SEPDBS(since 2021)
	  ```
	  ``` 
	  chase PM and Richard first(cc , timeline, after awhile, no progress, need to escalate:
	  \\UCEMPRDPFT\NTUCSAP\OCBC:  referenced in SAP,  wait response from fujitsu, not it is still used?
	  \\UCEMPRDPFT\NTUCSAP\Final_Payment_listing:  FINIX has a similar one  Final_Payment_listingOLD, checking Fujitsu for more info
	  ```
	- SFTP connection setup in FINIX: SAP retried, the connection still is not okay. (check with Richard what to do, check with status, find info to discuss, timeline)
	  background-color:: red
		- direct connect
		- **backup plans**:
			- sftp server is **public**,(need to test if FINIX can access it via internet as well, whitelists) access from  (using keys)
			- file synchronization between sftp server and UCEMPRODFT[**UTAP replatform**], azure and dpc both need slift licenses
			- smb
	- mentorship cnam setup:  Richard removed app gateway   mentorship--> app gw ->kinobi ( certificate issue)
		- app gateway and kinobi performance issues:
			- app gateway will connect to one server only. ( root causes at kinobi: not per-request load balancing, not cross-zone load balancing,  not optimized in nodejs app)
	- other things I have done this week: review utap-lite CR (updates in devops, adjust date)
	- blue/green deployment discussion:
		- efforts/costs: too long/cost (breakdown, more detailed, justify)
		- can schedule downtime
		- detailed comparison, analysis:  migrate to ASE
- meeting 2023-10-12
  collapsed:: true
	- IP info service info
		- ePayment: **202.176.197.212**:443	**202.176.197.146**:443, whitelisted in DBS RAPID
		- **202.176.197.150**(UCEMPRDPFT), whitelisted in DBS IDEAL Connect
	- bank gateway (SLIFT):
		- timeline for project
		- ``` 
		  \\UCEMPRDPFT\Report folder was used for unknown reason. verifying.
		  \\UCEMPRDPFT\UA_SFTPBox : requested to remove permission
		  
		  \\UCEMPRDPFT\DB-BKUP
		  \\UCEMPRDPFT\SEPDBS
		  \\UCEMPRDPFT\UP2_Report_Before2017
		  ```
		- ``` 
		  \\UCEMPRDPFT\NTUCSAP\OCBC:  referenced in SAP,  wait response from fujitsu, not it is still used?
		  \\UCEMPRDPFT\NTUCSAP\Final_Payment_listing:  FINIX has a similar one  Final_Payment_listingOLD, checking Fujitsu for more info
		  ```
	- Umatrix:
		- HSEU.ORG.SG:  Aleph still have an issue to map www.HSEU.ORG.SG to https://www.ntuc.org.sg/hseu
		- TPE VAPT
		  ![image.png](../assets/image_1697043503855_0.png){:height 319, :width 801}
	- PowerVA:
		- Study Power Visual Agent ChatBot: (have read)
		- design and implement bot (3 weeks)
		  SCHEDULED: <2023-11-03 Fri>
		- refine bot (topic tuning etc) ( 3 weeks)
		  SCHEDULED: <2023-11-24 Fri>
- meeting 2023-10-06
  collapsed:: true
	- bank gateway (SLIFT):
		- Richard asked dxc to check if need to buy an additional license , dxc team will confirm after the POC by next week.
		- Richard asked DXC for new estimated efforts, wait timeline info from dxc
		- TODO Richard started to check folders:
		  SCHEDULED: <2023-10-13 Fri>
		  ```
		  \\UCEMPRDPFT\DB-BKUP
		  \\UCEMPRDPFT\SEPDBS
		  \\UCEMPRDPFT\Report
		  \\UCEMPRDPFT\UP2_Report_Before2017
		  \\UCEMPRDPFT\UA_SFTPBox
		  ```
		- need Jenny's help on the two folders to move the sharing folder to a backup folders
		  SCHEDULED: <2023-10-13 Fri>
		  ```
		  \\UCEMPRDPFT\NTUCSAP\Final_Payment_listing
		  \\UCEMPRDPFT\NTUCSAP\OCBC
		  ```
	- UTAP: another way to change appsettings.json without restart; switch to **app config** for new projects
	  collapsed:: true
		- [Mount Azure Storage as a local share in App Service](https://learn.microsoft.com/en-us/azure/app-service/configure-connect-to-azure-storage?pivots=code-windows&tabs=basic%2Ccli#configure-your-app-with-azure-storage)
		- [reloadOnChange: true : The file is reloaded when changes are saved.](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-6.0#:~:text=Reads%20the%20default%20configuration%20providers%20before%20the%20MyConfig.json%20file.%20Settings%20in%20the%20MyConfig.json%20file%20override%20setting%20in%20the%20default%20configuration%20providers%2C%20including%20the%20Environment%20variables%20configuration%20provider%20and%20the%20Command%2Dline%20configuration%20provider)
		  
		  ```csharp
		  using Microsoft.Extensions.DependencyInjection.ConfigSample.Options;
		  
		  var builder = WebApplication.CreateBuilder(args);
		  
		  builder.Configuration.AddJsonFile("MyConfig.json",
		          optional: true,
		          reloadOnChange: true);
		  
		  builder.Services.AddRazorPages();
		  
		  var app = builder.Build();
		  ```
	- Umatrix:  I have shared my verification cases with Aleph and Francis. Hope they can run the tests before going live
		- wait for postmortem analysis from sitecore
		- raised no-cache issues to **Aleph**
		- verification cases:
		  
		  #+BEGIN_QUOTE
		  •	ga tags
		  •	search, should show contents within current microsites first in in-site search result page
		  •	google and Bing result:  [key words] site:www.ntuc.org.sg/[microsite]
		  •	download media extension name shown in the pages
		  •	any errors (in chrome console)
		  #+END_QUOTE
		- use for internal only
		  
		  ``` bash
		   jq -ncM '{method: "GET", url: "https://www.ntuc.org.sg/uportal/", body: "" | @base64, header: {"Content-Type": ["text/plain"]}}' | \
		   vegeta attack -format=json  -duration 60s -rate=50 |\
		   vegeta encode > ntuc.bin 2>&1
		   
		  cat ntuc.bin | vegeta report -type=hdrplot
		  
		  Value(ms)     Percentile  TotalCount  1/(1-Percentile)
		  0.114435      0.000000    0           1.000000
		  13649.917251  0.650000    3900        2.857143
		  15927.440722  0.700000    4200        3.333333
		  19400.654582  0.750000    4500        4.000000
		  21156.604337  0.775000    4650        4.444444
		  23590.121545  0.800000    4800        5.000000
		  27379.563961  0.825000    4950        5.714286
		  29996.411923  0.850000    5100        6.666667
		  30000.378501  0.875000    5250        8.000000
		  30000.466964  0.887500    5325        8.888889
		  30000.568558  0.900000    5400        10.000000
		  30000.676430  0.912500    5475        11.428571
		  30000.787162  0.925000    5550        13.333333
		  30000.900870  0.937500    5625        16.000000
		  30000.964009  0.943750    5663        17.777778
		  30001.004357  0.950000    5700        20.000000
		  ```
	- TODO power va:
	  collapsed:: true
		- Power Virtual Agents classic: too limit
		- AI-based: tested generative AI from https://web.test.powerva.microsoft.com/tryit?azure-portal=true for https://www.ntuc.org.sg/uportal/how-we-help, it is quite promising,  next week timeline
		  SCHEDULED: <2023-10-11 Wed>
			- https://www.ntuc.org.sg/uportal/how-we-help
	- TODO shared folder FINIX: big risk (step in, drive the work) **timeline** for NTUCSAP folders
	  collapsed:: true
		- talk in cloud meeting
	- DONE GA: how many complete, how left
	- TODO  external services & IPs : sharing info gathered
	  SCHEDULED: <2023-10-13 Fri>