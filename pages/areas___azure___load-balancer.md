- Azure Load Balancer distribution modes
	- <table aria-label="Azure Load Balancer distribution modes" class="table table-sm margin-top-none">
	  <thead>
	  <tr>
	  <th>Distribution mode</th>
	  <th>Hash based</th>
	  <th>Session persistence: Client IP</th>
	  <th>Session persistence: Client IP and protocol</th>
	  </tr>
	  </thead>
	  <tbody>
	  <tr>
	  <td>Overview</td>
	  <td>Traffic from the same client IP routed to any healthy instance in the backend pool</td>
	  <td>Traffic from the same client IP is routed to the same backend instance</td>
	  <td>Traffic from the same client IP and protocol is routed to the same backend instance</td>
	  </tr>
	  <tr>
	  <td>Tuples</td>
	  <td>five-tuple</td>
	  <td>two-tuple</td>
	  <td>three-tuple</td>
	  </tr>
	  <tr>
	  <td>Azure portal configuration</td>
	  <td>Session persistence: <strong>None</strong></td>
	  <td>Session persistence: <strong>Client IP</strong></td>
	  <td>Session persistence: <strong>Client IP and protocol</strong></td>
	  </tr>
	  <tr>
	  <td><a href="/en-us/rest/api/load-balancer/load-balancers/create-or-update#loaddistribution" data-linktype="absolute-path">REST API</a></td>
	  <td><code>"loadDistribution":"Default"</code></td>
	  <td><code>"loadDistribution":SourceIP</code></td>
	  <td><code>"loadDistribution":SourceIPProtocol</code></td>
	  </tr>
	  </tbody>
	  </table>
- Gateway Load Balancer: with third-party Network Virtual Appliances (NVAs)
- inbound connectivity
	- [Floating IP](https://learn.microsoft.com/en-us/azure/load-balancer/load-balancer-floating-ip):
	- High availability (HA) ports: a type of load balancing rule that provides an easy way to load-balance **all** flows that arrive on **all** ports of an internal standard load balancer. The load-balancing decision is made per flow. This action is based on the following five-tuple connection: source IP address, source port, destination IP address, destination port, and protocol