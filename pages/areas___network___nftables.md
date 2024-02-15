- netfilter hooks
  ![](https://people.netfilter.org/pablo/nf-hooks.png)
- File formats
	- output format 
	  
	  ``` nftables
	  #!/usr/sbin/nft -f
	  
	  define ntp_servers = { 84.77.40.132, 176.31.53.99, 81.19.96.148, 138.100.62.8 }
	  
	  #flush table nat
	  table ip nat {
	  	chain prerouting {
	  		type filter hook prerouting priority 0; policy accept;
	                  ip saddr $ntp_servers counter
	  	}
	  
	  	chain postrouting {
	  		type filter hook postrouting priority 100; policy accept;
	  	}
	  }
	  ```
	- scripted config format
	  
	  ``` bash
	  #!/usr/sbin/nft -f
	  
	  define ntp_servers = { 84.77.40.132, 176.31.53.99, 81.19.96.148, 138.100.62.8 }
	  
	  add table filter
	  add chain filter input { type filter hook input priority 0; }
	  add rule filter input ip saddr $ntp_servers counter
	  ```