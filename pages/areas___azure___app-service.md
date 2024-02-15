- **pricing tier**
	- **Shared compute**: **Free** and **Shared**
	- **Dedicated compute**: The **Basic**, **Standard**, **Premium**, **PremiumV2**, and **PremiumV3**: dedicated Azure VMs
	- **Isolated**: The **Isolated** and **IsolatedV2**: dedicated Azure VMs on dedicated Azure Virtual Networks, maximum scale-out capabilities
- Per-app scaling:
- Hybrid Connections: App Service Hybrid Connections enables your apps to make *outbound* calls to specified TCP endpoints. The endpoint can be on-premises, in a virtual network, or anywhere that allows outbound traffic to Azure on port 443.
	- built on the Azure Relay Hybrid Connections capability.
- kudu console
	- [Debug Console menu Item missing within Kudu on Azure App Services?](https://stackoverflow.com/questions/76507412/debug-console-menu-item-missing-within-kudu-on-azure-app-services)
- deployment types
	- multi-tenant public service hosts App Service plans in the Free, Shared, Basic, Standard, Premium, PremiumV2, and PremiumV3 pricing SKUs
	- single-tenant App Service Environment (ASE) hosts Isolated SKU App Service plans directly in your Azure virtual network
- networking
	- <table aria-label="Table 1" class="table table-sm">
	  <thead>
	  <tr>
	  <th>Inbound features</th>
	  <th>Outbound features</th>
	  </tr>
	  </thead>
	  <tbody>
	  <tr>
	  <td>App-assigned address</td>
	  <td>Hybrid Connections</td>
	  </tr>
	  <tr>
	  <td>Access restrictions</td>
	  <td>Gateway-required virtual network integration</td>
	  </tr>
	  <tr>
	  <td>Service endpoints</td>
	  <td>Virtual network integration</td>
	  </tr>
	  <tr>
	  <td>Private endpoints</td>
	  <td></td>
	  </tr>
	  </tbody>
	  </table>
	- vnet-integration
		- Routes
			- **Application** routing: defines what traffic is routed from your app and into the virtual network
			- **Configuration** routing: affects operations that happen before or during startup of your app.
			- **Network** routing: use route tables to route outbound traffic from your app without restriction. Common destinations can include firewall devices or gateways; use a [network security group](https://learn.microsoft.com/en-sg/azure/virtual-network/network-security-groups-overview) (NSG) to block outbound traffic to resources in your virtual network or the internet.
		- Gateway-required virtual network integration
	- [Get a static outbound IP](https://learn.microsoft.com/en-sg/azure/app-service/overview-inbound-outbound-ips#get-a-static-outbound-ip)
		- https://learn.microsoft.com/en-sg/azure/app-service/overview-vnet-integration#manage-virtual-network-integration
- ASE:  an Azure App Service feature that provides a fully isolated and dedicated environment for running App Service apps securely at high scale. a single-tenant deployment of Azure App Service
	- External ASE vs ILB ASE
		- With a VIP on an external public facing IP address, often called an **External** ASE.
		- With the VIP on an internal IP address, often called an **ILB** ASE because the internal endpoint is an Internal Load Balancer (ILB).
- [Azure Web App sandbox](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#app-service-plans-and-sandbox-limits) #inbox
- [App Service app settings](https://learn.microsoft.com/en-us/azure/app-service/configure-common?tabs=portal):