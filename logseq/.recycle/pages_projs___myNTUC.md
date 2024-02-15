- doc: https://sntuc.sharepoint.com/sites/TODataandTechnology/Shared%20Documents/Forms/AllItems.aspx?id=%2Fsites%2FTODataandTechnology%2FShared%20Documents%2FMember%20Platform&viewid=bdaae9dc%2Daaf9%2D4df5%2D94ca%2D3a985cb817e6&OR=Teams%2DHL&CT=1687168268120&clickparams=eyJBcHBOYW1lIjoiVGVhbXMtRGVza3RvcCIsIkFwcFZlcnNpb24iOiIyNy8yMzA1MDEwMDQyMiIsIkhhc0ZlZGVyYXRlZFVzZXIiOmZhbHNlfQ%3D%3D
- database: managed postgresql
- server: **Nodejs, prima**
- backend: hosted in Kubernetes
	- ```bash
	  kubectl  api-resources > api-resources.txt
	  kubectl get crd   > crd.txt
	  kubectl  get crd --output=custom-columns=NAME:.metadata.name  --no-headers |\
	     xargs -L1 -I{} sh -c "echo {};kubectl get {} -A -o json" > cust-resources.json
	  kubectl get pods -A -o json > pods.json
	  ```
- mobile app: flutter
- application-insights: backend-prd
- a.k.a.  membership platform.  its initial goal is to replace UCEM. however it never reach its goal.
- smsGatewaySenderName: NTUCMbrship
- issues:
	- MobSF
	- firebase dynamic link: will be shutdown on **August 25, 2025**
	- How to force users to update app
	- Fatal Exception: io.flutter.plugins.firebase.crashlytics.FlutterError 
	  HttpException: Software caused connection abort, uri = {:height 368, :width 640}. Error thrown Instance of 'CF'.
- order id algorithm
	- Get OrderID
	  Prefix by service type (OMA, OMR and OTH) + YEAR + (MONTH + 1) + (Day) + 6
	  digits of next clientorderID + 4 random hex string
	- prefixes
		- OMA = Membership sign-up
		- OMR = Arrears payment/renewal
		- OTH = Change payment mode, GIRO/CC recurring only
-
- [Membership auto-linking](https://dev.azure.com/sntuc/NTUC%20Member%20Platform/_workitems/edit/4115)