- One-stop system for U Care: https://ucare.ntuc.org.sg/assistance/
- sharepoint: https://sntuc.sharepoint.com/sites/itd/ItdOnly/Tender%20%20ITQ%20Document/Forms/AllItems.aspx?FolderCTID=0x012000E90FCF063FCBCC4A9B5A05363557F0A6&id=%2Fsites%2Fitd%2FItdOnly%2FTender%20%20ITQ%20Document%2F2021%20%2D%20NTUC%20TN2021005%20%2D%20Development%20and%20Maintenance%20of%20U%20Care%20Super%20System&viewid=cdecb781%2Dec64%2D4f50%2Daa59%2Df64b1ad0f30b
- U Care: Labour Movement’s fundraising efforts to better the welfare of low-income union members and their families
- email: [RE INC000022283493  SFTP IDs and Details.msg](https://sntuc.sharepoint.com/:u:/r/sites/itd/ItdOnly/Tender%20%20ITQ%20Document/2021%20-%20NTUC%20TN2021005%20-%20Development%20and%20Maintenance%20of%20U%20Care%20Super%20System/07%20Project%20Implementation/Reference/SFTP/RE%20INC000022283493%20%20SFTP%20IDs%20and%20Details.msg?csf=1&web=1&e=Bv0vyB)
- 10.101.248.4
- ``` bash
  # F22wicx7
  $ sftp -o HostKeyAlgorithms=+ssh-rsa  sftp://FusionEx_UCare_UAT@SFTP8822.ntuc.org.sg:8822
  ```
- search resources using onecare and ucare in sharepoint
- timeline https://mermaid.live/view#pako:eNptkMFqwzAMhl9F-JRCO7b0MszYodllh9BB6E6-OM7fxRDHwZY7Sum7z2026MZ0sRGfpE86CeM7CCnYOgx2hBopB1seQNsRlQ6gYk3G5xeriHCwBnExY-Waah1MT-X9Q0mSdnTl4zEyHBW7qlnQTP4OSa-bmj7RxqlHLjg8_k-lyQfWAz214fm7N1bvPplcFWkK_iNo53CXh8wNsk12KW9cmjQhUHM1-jNE0uatpmKbeBb-2eoGsFVqIZbCIThtu3yn04VRgns4KCHzt8Nep4GVUOM5ozqxb46jEZJDwlKkqdOMF6svrnPy_AU6LG1B
- modules:
	- programme management
	- donor management
	- education co-funding
- integration with SAP
	- https://sntuc.sharepoint.com/:p:/r/sites/itd/ItdOnly/_layouts/15/Doc.aspx?sourcedoc=%7BB3BFC61E-5E33-467C-8A2B-769F03E10DA6%7D&file=UCare_Connection%20updated.pptx&action=edit&mobileredirect=true
	- Flow
	  ```mermaid
	  sequenceDiagram
	      alt inbound
	          OneCare->>+SFTP: SFTP\UCARESuper_PRD\ <br>sap\inbox <br>collection/cc & egiro <br> evoucher/out & return
	          SFTP->>+UCEMPRDFT: wintel script job, copy files from sftp to <br> \\UCEMPRDPFT\NTUCSAP\UCare\Inbound
	          SAP ->>+UCEMPRDFT: poll for communication files
	      else outbound
	          SAP ->>+ UCEMPRDFT: put files
	          UCEMPRDFT->>+SFTP: wintel script job, copy files from \\UCEMPRDPFT\NTUCSAP\UCare\Outbound to <br> sftp
	          OneCare ->>+SFTP: pick up files in SFTP\UCARESuper_PRD\sap\oubox and processing
	      end
	  ```
	- target flow
	  
	  ``` mermaid
	  sequenceDiagram
	      alt inbound
	          OneCare->>+SFTP: SFTP\UCARESuper_PRD\ <br>sap\inbox <br>collection/cc & egiro <br> evoucher/out & return
	          SAP ->>+SFTP: poll for communication files
	      else outbound
	          SAP ->>+ SFTP: put files
	          OneCare ->>+SFTP: pick up files in SFTP\UCARESuper_PRD\sap\oubox and processing
	      end
	  
	  ```
	- SFTP\\UCARESuper_PRD\\sap\\inbox
		- ar, ap
	- SFTP\\UCARESuper_PRD\\sap\\outbox
		- ar, ap
- other sftp integrations
	- collection
		- cc
		- egiro
	- uniqgift
		- evoucher
			- out
			- return