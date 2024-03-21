- DynamoDB vs CosmosDB
  <table aria-label="Table 1" class="table table-sm margin-top-none">
  <thead>
  <tr>
  <th>DynamoDB</th>
  <th>Azure Cosmos DB</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <td>Not applicable</td>
  <td>Database</td>
  </tr>
  <tr>
  <td>Table</td>
  <td>Collection</td>
  </tr>
  <tr>
  <td>Item</td>
  <td>Document</td>
  </tr>
  <tr>
  <td>Attribute</td>
  <td>Field</td>
  </tr>
  <tr>
  <td>Secondary Index</td>
  <td>Secondary Index</td>
  </tr>
  <tr>
  <td>Primary Key – Partition key</td>
  <td>Partition Key</td>
  </tr>
  <tr>
  <td>Primary Key – Sort Key</td>
  <td>Not Required</td>
  </tr>
  <tr>
  <td>Stream</td>
  <td>ChangeFeed</td>
  </tr>
  <tr>
  <td>Write Compute Unit</td>
  <td>Request Unit (Flexible, can be used for reads or writes)</td>
  </tr>
  <tr>
  <td>Read Compute Unit</td>
  <td>Request Unit (Flexible, can be used for reads or writes)</td>
  </tr>
  <tr>
  <td>Global Tables</td>
  <td>Not Required. You can directly select the region while provisioning the Azure Cosmos DB account (you can change the region later)</td>
  </tr>
  </tbody>
  </table>
- Azure Cosmos DB provides language-integrated, transactional execution of JavaScript that lets you write stored procedures, triggers, and user-defined functions (UDFs).  in JavaScript
- <img src="https://learn.microsoft.com/en-us/azure/cosmos-db/media/choose-api/decision-tree.svg"></img>
- RNTBD:  intended to be the high-performance TCP transport alternative to HTTP for Cosmos. At its core, the transport stack must implement the `Microsoft.Azure.Documents.TransportClient` contract.
	- Accept requests intended for a Cosmos DB replica.
	- Serialize and send the requests to the intended endpoint ,
	- De-serialize the response and return a StoreResponse in a timely fashion or fail with an appropriate error.