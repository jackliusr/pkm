- environments
	- scope
	  collapsed:: true
		- under an Azure Active Directory (Azure AD) tenant, and its resources can only be accessed by users within that tenant.
		- bound to a geographic location
		- have zero or one Microsoft Dataverse database, for your apps and chatbots
		- app is only permitted to connect to the data sources that are also deployed in that same environment, including connections, gateways, flows, and Dataverse databases
		- move resources between environments
	- permissions
	  collapsed:: true
		- *Environment Admin*
		- *Environment Maker*
	- type of environments
	  collapsed:: true
		- <table aria-label="Table 1" class="table table-sm">
		  <thead>
		  <tr>
		  <th>Type</th>
		  <th>Description</th>
		  <th>Security</th>
		  </tr>
		  </thead>
		  <tbody>
		  <tr>
		  <td>Production</td>
		  <td>This is intended to be used for permanent work in an organization. It can be created and owned by an administrator or anyone with a Power Apps license, provided there is 1&nbsp;GB available database capacity. These environments are also created for each existing Dataverse database when it is upgraded to version 9.0 or later. Production environments are what you should use for any environments on which you depend.</td>
		  <td>Full control.</td>
		  </tr>
		  <tr>
		  <td>Default</td>
		  <td>These are a special type of production environment. Each tenant has a default environment that's created automatically. Its characteristics are discussed in the following section, <a href="#the-default-environment" data-linktype="self-bookmark">The default environment</a></td>
		  <td>Limited control. All licensed users<sup>1</sup> have the environment maker role.</td>
		  </tr>
		  <tr>
		  <td>Sandbox</td>
		  <td>These are non-production environments, which offer features like copy and reset. Sandbox environments are used for development and testing, separate from production. Provisioning sandbox environments can be restricted to admins (because production environment creation can be blocked), but converting from a production to a sandbox environment can't be blocked.</td>
		  <td>Full control. If used for testing, only user access is needed. Developers require environment maker access to create resources.</td>
		  </tr>
		  <tr>
		  <td>Trial</td>
		  <td>Trial environments are intended to support short-term testing needs and are automatically cleaned up after a short period of time. They expire after 30 days and are limited to one per user. Provisioning trial environments can be restricted to admins.</td>
		  <td>Full control.</td>
		  </tr>
		  <tr>
		  <td>Developer</td>
		  <td>Developer environments are created by users who have the Developer Plan license. They're special environments intended only for use by the owner. Provisioning developer environments can be restricted to admins. More information: <a href="control-environment-creation#developer-environments" data-linktype="relative-path">Control environment creation</a>. The developer environment will be available as long as you actively use the Power Apps Developer Plan. More information: <a href="/en-us/powerapps/maker/developer-plan" data-linktype="absolute-path">Power Apps Developer Plan</a></td>
		  <td>Limited control.  Security groups can't be assigned to developer environments.</td>
		  </tr>
		  <tr>
		  <td>Microsoft Dataverse for Teams</td>
		  <td>Dataverse for Teams environments are automatically created for the selected team when you create an app in Teams using the app for the first time or install an app from the app catalog. More information: <a href="about-teams-environment" data-linktype="relative-path">About the Dataverse for Teams environment</a>.</td>
		  <td>Limited control. Admins have limited settings available for Teams environments. No customizations of security role or assignments are available. Teams members are automatically mapped to their Teams membership type - owners, members, and guests - with a corresponding security role assigned by the system.</td>
		  </tr>
		  </tbody>
		  </table>
- [Detail Checklist to set up Power Platform Governance](https://powerusers.microsoft.com/t5/Power-Apps-Community-Blog/Detail-Checklist-to-set-up-Power-Platform-Governance/ba-p/2158415)
- Microsoft Power Platform In a Day workshops
- [Microsoft Dataverse teams management](https://learn.microsoft.com/en-us/power-platform/admin/manage-teams)
	- type of teams
		- **Owner team**: An *owner team* owns records and has security roles assigned to the team.
		- **Access team:** An *access team* doesn't own records and doesn't have security roles assigned to the team.
		- **Azure AD group team**
- Governance
- Managed Environments: a suite of premium capabilities that allows admins to manage Power Platform at scale with more control, less effort, and more insights
- refresh cadences
- Power Platform and Azure Logic Apps connectors