- quickway to locate not-tracked sites
  ``` bash
  # quick get download index/home pages and grep for ga trackid
  # one line, one url in sites.txt
  # sample line in sites.txt
  # https://www.ntuc.org.sg/ausbe
  cat <<EOF >sites.txt
  https://www.ntuc.org.sg/dbssu
  https://www.ntuc.org.sg/ucarecentre
  https://www.ntuc.org.sg/pubeu
  https://www.ntuc.org.sg/smeeu
  https://www.ntuc.org.sg/sube
  https://www.ntuc.org.sg/srceu
  EOF
  #sort -o sites.txt sites.txt
  sort -o sites.txt{,}
  wget -x -i sites.txt
  # assume that all the microsites are hosted under https://www.ntuc.org.sg
  grep  -irn "gtag('config'"   www.ntuc.org.sg/* | grep 'G-9W180N3VPB' | grep -Eo 'www.ntuc.org.sg\/\w*' | sort | uniq >ga4.txt
  # remove https:// in sites.txt
  sed -i -E 's/^\s*.*:\/\///g' sites.txt
  # get all sites which don't have GA4 tags
  diff -y sites.txt ga4.txt | grep '<'
  ```
- DOING https://dev.azure.com/sntuc/TA%20Board/_workitems/edit/5170 /target
  DEADLINE: <2023-06-09 Fri>
  :LOGBOOK:
  CLOCK: [2023-06-09 Fri 23:37:52]
  :END:
- two properties. one for aggregated reports, another for individual sites/microsites.
- GA Migration:
	- issue in GA4:  how to manage permissions for NTUC and UNION as there is no equivalent view level permissions.
		- UA: view level permissions to unions and NTUC.
		- possible solutions:
			- multiple GA4 Configuration tags in a single Google Tag Manager (GTM) container FREE
				- properties per union (domain, subpath: microsite, landing page etc)
				- NTUC
			- google analytics 360: ** $150,000 per year and billed at $12,500 a month**
			- other? not sure, ask Aleph