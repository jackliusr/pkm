- **Storage account type**
  <table aria-label="Types of storage accounts" class="table">
  <thead>
  <tr>
  <th>Storage account type</th>
  <th>Performance tier</th>
  <th>Usage</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <td>General-purpose v2</td>
  <td>Standard</td>
  <td>Standard storage account type for blobs, file shares, queues, and tables. Recommended for most scenarios using Blob Storage or one of the other Azure Storage services.</td>
  </tr>
  <tr>
  <td>Block blob</td>
  <td>Premium</td>
  <td>Premium storage account type for block blobs and append blobs. Recommended for scenarios with high transaction rates or that use smaller objects or require consistently low storage latency</td>
  </tr>
  <tr>
  <td>Page blobs</td>
  <td>Premium</td>
  <td>Premium storage account type for page blobs only.</td>
  </tr>
  </tbody>
  </table>
- access tier: hot, cool, cold, archive
	- considerations:
		- The access tier can be set on a blob **during or after upload**.
		- Only the **hot and cool** access tiers can be set at the **account** level. The **archive** access tier can only be set at the **blob** level.
		- Data in the **cool** access tier has slightly lower availability, but still has high durability, retrieval latency, and throughput characteristics similar to hot data.
		- Data in the archive access tier is stored **offline**. The archive tier offers the lowest storage costs but also the highest access costs and latency.
		- The hot and cool tiers support all **redundancy options**. The archive tier supports only **LRS, GRS, and RA-GRS**.
		- Data storage **limits** are set at the **account level** and not per access tier. You can choose to use all of your limit in one tier or across all three tiers.
- storage account: http://mystorageaccount.blob.core.windows.net
- container: https://myaccount.blob.core.windows.net/mycontainer
- blob:
	- block blob:  made up of **blocks** of data that can be managed individually. Block blobs can store up to about 190.7 TiB.
	- append blob
	- page blob: random access files up to 8 TB in size. Page blobs store virtual hard drive (VHD) files and serve as disks for Azure virtual machines
- static website hosting: *$web*
	- custom domain
	- limitations:
		- no way to configure headers
		- AuthN and AuthZ aren't supported
- lifecycle:
	- rule-based policy for **General Purpose v2 and Blob storage accounts**
	- lifecycle management policy
	  collapsed:: true
		- rules
		- rules filter
		- rule actions
		- sample: 
		  
		  ``` json
		  {
		    "rules": [
		      {
		        "name": "ruleFoo",
		        "enabled": true,
		        "type": "Lifecycle",
		        "definition": {
		          "filters": {
		            "blobTypes": [ "blockBlob" ],
		            "prefixMatch": [ "container1/foo" ]
		          },
		          "actions": {
		            "baseBlob": {
		              "tierToCool": { "daysAfterModificationGreaterThan": 30 },
		              "tierToArchive": { "daysAfterModificationGreaterThan": 90 },
		              "delete": { "daysAfterModificationGreaterThan": 2555 }
		            },
		            "snapshot": {
		              "delete": { "daysAfterCreationGreaterThan": 90 }
		            }
		          }
		        }
		      }
		    ]
		  }
		  ```
	- Rehydrate blob data from the archive
		- priority: `x-ms-rehydrate-priority` header
		- 2 options:
			- Copy an archived blob to an online tier
			- Change a blob's access tier to an online tier
- azcopy
	- AzCopy v10 by default uses 8MB block sizes.
	- block-size flag