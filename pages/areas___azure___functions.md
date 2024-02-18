- Azure Functions is built on the WebJobs SDK, so it shares many of the same event triggers and connections to other Azure services.
- hosting plans： **Consumption**，**Premium**，**Dedicated**
- hosting options: **ASE**, kubernetes(direct, or Arc)
- Function app timeout duration: host.json
- requires a general Azure Storage account, which supports Azure Blob, Queue, Files, and Table storage.
- scaling
	- scale in & scale out
	- cold start
	- Scaling behaviours: new instance rate (http: one/s, non-http: at most one per 30 seconds
	- functionAppScaleLimit
	- *scale controller*
	  ![](https://learn.microsoft.com/en-us/training/wwl-azure/explore-azure-functions/media/central-listener.png)
- Functions vs Logic Apps
  <table aria-label="Compare Azure Functions and Azure Logic Apps" class="table">
  <thead>
  <tr>
  <th></th>
  <th scope="col">Azure Functions</th>
  <th scope="col">Logic Apps</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <th scope="row">Development</th>
  <td>Code-first (imperative)</td>
  <td>Designer-first (declarative)</td>
  </tr>
  <tr>
  <th scope="row">Connectivity</th>
  <td>About a dozen built-in binding types, write code for custom bindings</td>
  <td>Large collection of connectors, Enterprise Integration Pack for B2B scenarios, build custom connectors</td>
  </tr>
  <tr>
  <th scope="row">Actions</th>
  <td>Each activity is an Azure function; write code for activity functions</td>
  <td>Large collection of ready-made actions</td>
  </tr>
  <tr>
  <th scope="row">Monitoring</th>
  <td>Azure Application Insights</td>
  <td>Azure portal, Azure Monitor logs</td>
  </tr>
  <tr>
  <th scope="row">Management</th>
  <td>REST API, Visual Studio</td>
  <td>Azure portal, REST API, PowerShell, Visual Studio</td>
  </tr>
  <tr>
  <th scope="row">Execution context</th>
  <td>Runs in Azure, or locally</td>
  <td>Runs in Azure, locally, or on premises</td>
  </tr>
  </tbody>
  </table>
- Functions vs Webjobs
  <table aria-label="Compare Functions and WebJobs" class="table">
  <thead>
  <tr>
  <th></th>
  <th scope="col">Functions</th>
  <th scope="col">WebJobs with WebJobs SDK</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <th scope="row">Serverless app model with automatic scaling</th>
  <td>Yes</td>
  <td>No</td>
  </tr>
  <tr>
  <th scope="row">Develop and test in browser</th>
  <td>Yes</td>
  <td>No</td>
  </tr>
  <tr>
  <th scope="row">Pay-per-use pricing</th>
  <td>Yes</td>
  <td>No</td>
  </tr>
  <tr>
  <th scope="row">Integration with Logic Apps</th>
  <td>Yes</td>
  <td>No</td>
  </tr>
  <tr>
  <th scope="row">Trigger events</th>
  <td>Timer<br>Azure Storage queues and blobs<br>Azure Service Bus queues and topics<br>Azure Cosmos DB<br>Azure Event Hubs<br>HTTP/WebHook (GitHub<br>Slack)<br>Azure Event Grid</td>
  <td>Timer<br>Azure Storage queues and blobs<br>Azure Service Bus queues and topics<br>Azure Cosmos DB<br>Azure Event Hubs<br>File system</td>
  </tr>
  </tbody>
  </table>