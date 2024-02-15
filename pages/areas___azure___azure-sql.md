- reserved instance for serveless , **elastic pool** database?
- Elastic database transaction units (eDTUs)
- Elastic job
	- <table aria-label="Table 1" class="table table-sm">
	  <thead>
	  <tr>
	  <th></th>
	  <th scope="col">Elastic Jobs</th>
	  <th scope="col">SQL Agent</th>
	  </tr>
	  </thead>
	  <tbody>
	  <tr>
	  <th scope="row">Scope</th>
	  <td>Any number of databases in Azure SQL Database and/or data warehouses in the same Azure cloud as the job agent. Targets can be in different servers, subscriptions, and/or regions (dynamically enumerated at job runtime).</td>
	  <td>Any individual database in the same instance as the SQL agent. The Multi Server Administration feature of SQL Server Agent allows for master/target instances to coordinate job execution, though this feature is not available in SQL managed instance.</td>
	  </tr>
	  <tr>
	  <th scope="row">Supported APIs and Tools</th>
	  <td>Portal, PowerShell, T-SQL, Azure Resource Manager</td>
	  <td>T-SQL, SQL Server Management Studio (SSMS)</td>
	  </tr>
	  </tbody>
	  </table>
	- <table aria-label="Table 2" class="table table-sm">
	  <thead>
	  <tr>
	  <th>Component</th>
	  <th>Description (additional details are below the table)</th>
	  </tr>
	  </thead>
	  <tbody>
	  <tr>
	  <td><a href="#elastic-job-agent" data-linktype="self-bookmark"><strong>Elastic Job agent</strong></a></td>
	  <td>The Azure resource you create to run and manage Jobs.</td>
	  </tr>
	  <tr>
	  <td><a href="#elastic-job-database" data-linktype="self-bookmark"><strong>Job database</strong></a></td>
	  <td>A database in Azure SQL Database that the job agent uses to store job related data, job definitions, etc.</td>
	  </tr>
	  <tr>
	  <td><a href="#target-group" data-linktype="self-bookmark"><strong>Target group</strong></a></td>
	  <td>The set of servers, pools, and databases to run a job against.</td>
	  </tr>
	  <tr>
	  <td><a href="#elastic-jobs-and-job-steps" data-linktype="self-bookmark"><strong>Job</strong></a></td>
	  <td>A job is a unit of work that is composed of one or more job steps. Job steps specify the T-SQL script to run, as well as other details required to execute the script.</td>
	  </tr>
	  </tbody>
	  </table>