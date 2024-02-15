link:: https://dev.azure.com/sntuc/TA%20Board/_workitems/edit/5688

- best practices on zero downtime
- dxc agenda during discussion:
	- a. Implementation of blue-green strategy (how to verify , which components ?)
	- b. SSL upgrade optimization
	- c. Review MyNTUC architecture flow and discuss on few proposal for re-architecting
- **Pre-requisite**
	- .cer file and .pfx file is given by NTUC ( script need to generate pfx)
	- .cer file contains 3 certificates (main cert, intermittent cert and root cert) and a private key (script & automation)
	- Places to update SSL cert in this order (why item 2? apim is not enough?)
		- Azure keyvault (DXC-MYNTUC)
		  logseq.order-list-type:: number
		- ntuc-member-app-backend (DXC-MYNTUC)
		  logseq.order-list-type:: number
		- **Azure Application Gateway (NTUC)** : exposed to public
		  logseq.order-list-type:: number
		- **Azure APIM (DXC-MYNTUC)**: exposed to public
		  logseq.order-list-type:: number
- runbook: rundesk, pagerduty etc, automate above process
- pipeline:
- **Web-Agent**?  later renamed to e-check
- Runbooks:
	- https://dev.azure.com/sntuc/NTUC%20Member%20Platform/_wiki/wikis/NTUC-Member-Platform.wiki/263/SSL-Upgrade
		- lack of verifying the date
		  
		  ``` bash
		  openssl s_client -connect 20.184.61.20:443 -servername ma.ntuc.org.sg -showcerts |\
		    grep -iA2 "Validity"
		  ```
	- https://dev.azure.com/sntuc/NTUC%20Member%20Platform/_wiki/wikis/NTUC-Member-Platform.wiki?friendlyName=SSL-Update-Runbook&pagePath=/NTUC%20Member%20Platform/SSL%20Upgrade/SSL%20Upgrade%20for%20MP%20(DEV%20and%20UAT)
- recent issues:
	- full chain verification,
	- validate check don't check the date part (overlapped start date and end date, use it before another one is expired)
	  
	  ```bash
	   openssl s_client -connect apim.ntuc.org.sg:443 < /dev/null 2>/dev/null  |\
	    openssl x509 -dates -noout -in /dev/stdin
	  ```
	- forget to update 6 endpoints in k8s,
	- too long to take effects
		- aks? don't take too long from my past experiences.
		- certificate automation
		- [certificates in keyvault, apim](https://learn.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates-for-clients#:~:text=Certificates%20updated%20in%20the%20key%20vault%20are%20automatically%20rotated%20in%20API%20Management.%20After%20update%20in%20the%20key%20vault%2C%20a%20certificate%20in%20API%20Management%20is%20updated%20within%204%20hours.%20You%20can%20also%20manually%20refresh%20the%20certificate%20using%20the%20Azure%20portal%20or%20via%20the%20management%20REST%20API.)
	- questions: ?
		- cert-manager  used ?  need to find out
		- app gateway: https://dev.azure.com/sntuc/NTUC%20Member%20Platform/_wiki/wikis/NTUC-Member-Platform.wiki/265/SSL-Upgrade-for-MP-(DEV-and-UAT)#:~:text=To%20be%20done%20by%20NTUC%2C%20we%20only%20need%20to%20check%20if%20they%20uploaded%20the%20certs%20on%20application%20gateway%20and%20myntuc%2Dadmdev.ntuc.org.sg%20or%20myntuc%2Dadmuat.ntuc.org.sg
		- ssl termination/offloading at app-gw? plain internal?
		- use autorotated certs for communications for mTLS between app-gw and k8s ingress
	- practices:
		- Runbook: include misconfig case, troubeshooting, step-by-steps instructions without other references
			- one prepare , one run to test if it work
		- drill excercises
		- script as much as possible for verify certs (validation, start date & end date,  different endpoints where certs are updated)
			- ``` bash
			  openssl verify -no-CAfile -no-CApath -partial_chain -trusted RootCert.pem Intermediate.pem
			  ```
		- certificate in CSI secrets
		- call API to force to refresh certs from keyvault in apim:
			- how to refresh https://learn.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates#add-a-key-vault-certificate:~:text=Certificates%20updated%20in%20the%20key%20vault%20are%20automatically%20rotated%20in%20API%20Management.%20After%20update%20in%20the%20key%20vault%2C%20a%20certificate%20in%20API%20Management%20is%20updated%20within%204%20hours.%20You%20can%20also%20manually%20refresh%20the%20certificate%20using%20the%20Azure%20portal%20or%20via%20the%20management%20REST%20API.
			- https://learn.microsoft.com/en-us/rest/api/apimanagement/current-ga/certificate/refresh-secret?tabs=HTTP
		- automate runbooks with Rundeck liked tools
		- **Postmortem** analysis and update runbooks
		- copy & paste are error-prone: you can find many issues with this way:
		  collapsed:: true
			- https://www.google.com/search?q=ssh+terminal+copy+paste+character+error&safe=active&sca_esv=566856875&rlz=1C1GCEB_enSG1061SG1061&sxsrf=AM9HkKm1OZQJdcr37LF7AQP_4mFoAap5eA%3A1695196494472&ei=TqUKZf-7HP-f4-EPn5G32Ao&oq=ssh+terminal+copy+paste+chara&gs_lp=Egxnd3Mtd2l6LXNlcnAiHXNzaCB0ZXJtaW5hbCBjb3B5IHBhc3RlIGNoYXJhKgIIATIHECEYoAEYCjIHECEYoAEYCjIHECEYoAEYCkjIWFCeC1jjR3ADeAGQAQGYAbERoAHMZaoBEzAuMS40LjQuMS4yLjEuMC4yLjK4AQPIAQD4AQHCAgoQABhHGNYEGLADwgIEECMYJ8ICCBAAGIoFGJECwgILEAAYgAQYsQMYgwHCAhEQLhiABBixAxiDARjHARjRA8ICBxAuGIoFGEPCAgcQABiKBRhDwgIOEAAYigUYsQMYgwEYkQLCAgUQABiABMICCxAuGIAEGMcBGNEDwgILEC4YgAQYxwEYrwHCAgoQABiABBgUGIcCwgIGEAAYFhgewgIIEAAYigUYhgPCAgUQIRigAcICCBAhGBYYHhgdwgIEECEYFeIDBBgAIEGIBgGQBgI&sclient=gws-wiz-serp
- Postmortem/RCA reports
	- https://dev.azure.com/sntuc/NTUC%20Member%20Platform/_wiki/wikis/NTUC-Member-Platform.wiki/275/Incident-01-Private-Key-Mismatch
	- NTUC-INC24082428 - MyNTUC-SSL_Upgrade_issue_S1_v1.0.docx
- flow:
	- add response headers at apim, app-gw and ingress/ingress controller to prove this, **how to verify client**
	  ``` mermaid
	  flowchart TD
	     mobile-app[mobile-app: cert fingerprints] --> apim[itd-app-apim-prd-sea: apim.ntuc.org.sg 20.198.191.99, pfx cert in keyvault]
	     mobile-app --> app-gw[itd-alzcs-applgw02-prd-sea ma or myntuc-admin  20.184.61.20, pfx cert in uploaded file, layer7]
	     apim --> app-gw
	     app-gw -->|e2e TLS| k8s-lb[k8s-lb: kubernetes-internal layer 4]
	     k8s-lb --> k8s-ingress-controller[k8s ingresses in k8s-ingress-controller, PEM certs in k8s secrets]
	     browser --> app-gw
	     k8s-ingress-controller --> k8s-svc
	     k8s-svc --> k8s-pods
	  ```
	- mobile --> apim(**apim.ntuc.org.sg**) [https://ma.ntuc.org.sg/api/] ->app gw(itd-alzcs-applgw02-prd-sea)-> k8s ingress
	- mobile--> app gw -> k8s
		- app gw
			- backend pool: itd-memberapp-kubesvc-prd-sea-backend --> target 10.101.1.254 (k8s internal load balancer, frontend IP config)
			- listener (80,443) : **ma.ntuc.org.sg**
- fingerprint
	- check fingerprint
	  ``` bash
	  # launch.json
	  # dev https://apimdev.ntuc.org.sg/api
	  # dev-profile https://apimdev.ntuc.org.sg/api
	  # uat https://apimuat.ntuc.org.sg/api
	  # preprod https://apimpre.ntuc.org.sg/api
	  # prod https://apim.ntuc.org.sg/api
	  
	  # extract cert
	  openssl s_client -connect apim.ntuc.org.sg:443 2>/dev/null </dev/null | \
	   sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p'
	  # get public key 
	  openssl x509 -pubkey -noout -in cert.pem  > pubkey.pem
	  
	  # 7E:81:78:0A:B2:19:0A:2E:74:3A:12:36:F5:18:0D:8B:46:94:83:8E:38:B9:55:2B:29:38:6D:F0:B3:8E:E8:67
	  # 7e81780ab2190a2e743a1236f5180d8b4694838e38b9552b29386df0b38ee867
	  openssl s_client -connect apim.ntuc.org.sg:443 < /dev/null 2>/dev/null | \
	  openssl x509 -noout -fingerprint -sha256  -inform pem -in  /dev/stdin  |\
	   sed -e 's/://g' -e 's/\(.*\)/\L\1/'  -e 's/^[^=]*=//'
	   
	  # https://www.openssl.org/docs/man1.1.1/man1/openssl-x509.html#:~:text=Calculates%20and%20outputs,be%20the%20same. 
	  ```
	- batch check fingerprint
	  
	  ``` bash
	  cat <<EOF | \
	  xargs  -I{}  sh -c "echo {};openssl s_client -connect {}:443 < /dev/null 2>/dev/null |openssl x509 -noout -fingerprint -sha256  -inform pem -in  /dev/stdin  | sed -e 's/://g' -e 's/\(.*\)/\L\1/'  -e 's/^[^=]*=//'"
	  apimdev.ntuc.org.sg
	  apimuat.ntuc.org.sg
	  apimpre.ntuc.org.sg
	  apim.ntuc.org.sg
	  devma.ntuc.org.sg
	  uatma.ntuc.org.sg
	  prema.ntuc.org.sg
	  ma.ntuc.org.sg
	  myntuc-admuat.ntuc.org.sg
	  myntuc-adm.ntuc.org.sg
	  EOF
	  ```
	- Cert Pinning by sha265 **cert fingerprint**:
		- 94a13ac81 2022-02-25
		- embedded fingerprints into applications
		- ``` bash
		  git tag --contains 94a13ac81  
		  //appstore: 3.0.1 7 Apr 2022
		  //google play: 
		  
		  //source code https://github.com/ntuc-member-app/ntuc-mobile-app/commit/ba9e75fc754951f469db2e41c017334a9db41733
		  "SSL_FINGERPRINT=7e81780ab2190a2e743a1236f5180d8b4694838e38b9552b29386df0b38ee867,121affc5550ec52c58ccf9251e53b4db930bb2388ac095a23398ccd8e8c494af"
		  ```
		- finding 1
		  
		  ```dart
		  // commit: * (HEAD detached at v3.3.2-prod.173) ba9e75fc add SSL for new 2024 cert
		  
		  // line range: 
		  // https://github.com/ntuc-member-app/ntuc-mobile-app/blob/ba9e75fc754951f469db2e41c017334a9db41733/lib/di/injection_container.dart#L85C3-L95
		  // injection_container.dart
		    sl.registerLazySingleton(
		      //sl() will resolve to AppDio
		      () => BaseHttpClient(sl(), baseUrl: sl<AppConfig>().apiBaseUrl),
		    );
		    // dio
		    sl.registerLazySingleton<BaseOptions>(() => AppDio.baseOptions);
		    sl.registerLazySingleton(() => AppDio(
		          sl(),
		          sl(),
		          sslFingerprints: appConfig.sslFingerprints,
		          options: sl(),
		        ));
		  ```
		- finding 2
		  
		  ``` dart
		  // https://github.com/ntuc-member-app/ntuc-mobile-app/blob/ba9e75fc754951f469db2e41c017334a9db41733/lib/core/network/api/api_interceptor.dart#L36-L39
		  //api_interceptor.dart
		   interceptors.add(CertificatePinningInterceptor(
		        allowedSHAFingerprints: sslFingerprints,
		        timeout: 30,
		      ));
		  ```
- steps:
	- 1. [validate the full cerificate chain before deployment](https://docs.apigee.com/how-to-guides/validating-certificate-chain) ?
	- 2. simulate in UAT env