- [The Essential CDN Guide](https://www.imperva.com/learn/performance/cdn-guide/)
	- CDN Architecture
	  collapsed:: true
		- The Four Pillars of CDN design
			- performance
			- scalability
			- reliablity
			- responsiveness
		- CDN Topology
			- Scattered CDN
			- Consolidated CDNs
		- scrubbing center: A centralized data cleansing station where traffic is analyzed and malicious traffic (ddos, known vulnerabilities and exploits) is removed.
		- Push CDNs and Pull CDNs
	- Caching
	  collapsed:: true
		- Caching Algorithms
			- $$\text{average memory reference time(T)} = (1 - \text{Hit ratio}) \times (\text{Access time on miss}) +(\text{Access time on hit}) + (\text{Secondary latency factors})$$
			- Bélády’s Algorithm
			- Least Recently Used (LRU)
			- Most Recently Used (MRU)
		- cache busting
	- Front End Optimization
	  collapsed:: true
		- Progressive rendering
	- CDN and SSL/TLS
	- Route Optimization
		- Leveraging **anycast** for connection route optimization.
		- Providing privileged access to the Internet backbone.
			- The Tier 1 Shortcut
			- network peering
- Tiered Caching
- [cache busting](https://www.keycdn.com/support/what-is-cache-busting)
	- a technique used by web developers to force the browser to load the most recent version of a file, rather than a previously cached version.
	- **How to use cache busting?**
		- File name versioning
		- File path versioning
		- Query strings
- [Understanding CDN DNS Routing – Unicast Versus Anycast](https://blog.cdnsun.com/understanding-cdn-dns-routing-unicast-versus-anycast/)
- other technologies:
	- customized built linux
	- user-space network stack
	- special network card
	- kernel TLS
- multi-cdn
	- How does Multi CDN work?
		- DNS load balancing
		- Primary-Fallback Scheme
		- Performance data-driven load balancing
		- Turnkey Multi CDN platform
- cloudflare
	- Orpheus: builds and provisions routes from Cloudflare to origins by analyzing data from users on every path from Cloudflare and ordering them on a per-data center level with the goal of eliminating connection errors and minimizing packet loss. If Orpheus detects errors on the current path from Cloudflare back to a customer origin, Orpheus will steer subsequent traffic from the impacted network path to the healthiest path available.
	  ![](https://blog.cloudflare.com/content/images/2021/09/pasted-image-0--1-.png){:height 356, :width 619}