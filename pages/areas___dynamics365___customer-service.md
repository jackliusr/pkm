- `case management` is the core record that tracks individual customer service issues across channels and agents over time
- [Customer Service Learning Catalog](https://learn.microsoft.com/en-us/dynamics365/customer-service/learning-catalog)
- agent- productivity tools
	- macros
	- agent scripts
	- smart assist
	- microsoft teams
- Service Scheduling
- [Penetration Testing for Dynamics 365 (CRM)](https://community.dynamics.com/forums/thread/details/?threadid=59c381f0-d734-4c91-8e34-f296e2aae054)
- typescript, javascript
- access control
  collapsed:: true
	- [Record-based security](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/security-dev/use-record-based-security-control-access-records?view=op-9-1)
	- [Shared access](https://learn.microsoft.com/en-us/power-platform/admin/how-record-access-determined#shared-access)
		- <table aria-label="Table 3" class="table table-sm">
		  <tr>
		  <td><strong>The record was shared with the user directly</strong></td>
		  <td>If a record is shared with the user to perform a certain action, then the user would have access to do that action provided the user passed the privilege check.</td>
		  </tr>
		  <tr>
		  <td><strong>A related record was shared with the user directly</strong></td>
		  <td>The following scenario takes place when a record A is related to a record B. If the user has shared access to perform a certain action on the record A, it would then have inherited access to perform the same action on the record B, provided the user passed the privilege check.</td>
		  </tr>
		  <tr>
		  <td><strong>The record was shared with a team that the user belongs to</strong></td>
		  <td>If a record is shared with a team to perform a set of actions, then the users that belong to that team would have access to do those actions provided they passed the privilege check.</td>
		  </tr>
		  <tr>
		  <td><strong>A related record was shared with a team that the user belongs to</strong></td>
		  <td>The following scenario takes place when a record A is related to a record B. If record A is shared with a team to perform a set of actions, and record A is related to record B, then the users that belong to that team would have access to do those actions in both records A and B, provided they passed the privilege check.</td>
		  </tr>
		  <tr>
		  <td><strong>The record was shared with the entire organization</strong></td>
		  <td>If a record is shared with an organization to perform a set of actions, then all the users that belong to that organization will be able to perform those actions provided they passed the privilege check.</td>
		  </tr>
		  </tbody>
		  </table>
	- [field-level security](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/security-dev/use-field-security-control-access-field-values?view=op-9-1)
	  https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/media/crm-v5s-sm-fieldlevelsecurity.png?view=op-9-1
	- [hierarchical security](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/security-dev/hierarchical-security-control-access-entities?view=op-9-1)
- TODO: business rules and recommendations
- Hosted Application Toolkit (HAT) Software Factory
- Hosted Application Toolkit (HAT) architecture
- TODO action vs plugin vs workflow vs process vs CodeActivity
	- https://learn.microsoft.com/en-us/power-apps/developer/data-platform/workflow/workflow-extensions
	- https://learn.microsoft.com/en-us/power-apps/developer/data-platform/apply-business-logic-with-code?view=op-9-1
- MetaDiagramConsole.exe: allows you to generate Visio diagrams of entity relationship mappings, don't have descriptions of entities.
	- TODO: how to link visio to entity description, interactive diagram ?
- Customer support swarming: particularly useful when you need to do the following
	- Collaborate with experts across your organization to get help on complex cases.
	- Use an expert finder to quickly locate experts with the right skills to help.
- Dynamics 365 Channel Integration Framework version 2.0 provides an extensible framework to integrate third-party Computer Telephony Integration (CTI) systems to serve your customers with more focus and agility
  ![](https://learn.microsoft.com/en-us/dynamics365/customer-service/channel-integration-framework/media/cif-high-level-architecture-v2.png){:height 280, :width 636}