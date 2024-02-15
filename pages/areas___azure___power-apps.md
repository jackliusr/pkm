- license mode:
- [release planner](https://releaseplans.microsoft.com/en-US/?app=Power+Apps)
- components
	- index.ts: four essential functions (init, updateView , getOutputs, and destroy)
- https://carldesouza.com/creating-custom-workflow-activities-workflow-extensions-in-dynamics-365-and-powerapps/
	- create CodeActivity
	- Open the Plugin Registration Tool (PRT), and select Register->Register New Assembly:
	- Dynamics 365 / PowerApps and create a new Workflow to use the CodeActivity
- [Reference Architecture and Landing Zones for Power Platform](https://cloudblogs.microsoft.com/powerplatform/2022/02/18/north-star-architecture-and-landing-zones-for-power-platform/)
- A `connector` is a proxy or a wrapper around an API that allows the underlying service to talk to [Microsoft Power Automate](https://flow.microsoft.com/), [Microsoft Power Apps](https://powerapps.microsoft.com/), and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps). It provides a way for users to connect their accounts and leverage a set of prebuilt [*actions*](https://learn.microsoft.com/en-us/connectors/connectors#actions) and [*triggers*](https://learn.microsoft.com/en-us/connectors/connectors#triggers) to build their apps and workflows.
	- architecture: 
	  ![](https://learn.microsoft.com/en-us/connectors/architecture.png){:height 372, :width 585}
- User experience extensibility
	- Power Apps Code components: are implemented using HTML, CSS, and TypeScript. While not required that you use any particular UI Framework, [React](https://reactjs.org/) is a popular choice
	  collapsed:: true
		- type: Field, dataset
		- Component composition: a Manifest Input File, its implementation, and any additional resource files that might be needed by the component.
		  ![](https://learn.microsoft.com/en-us/training/modules/get-started-component-framework/media/key-areas.png){:height 328, :width 459}
		- lifecycle
		  | Method | Description |
		  | ---- | ---- | ---- |
		  | init | Required. This method is used to initialize the component instance. Components can kick off remote server calls and other initialization actions in this method. Dataset values cannot be initialized with this method; you will need to use the updateView method for this purpose. |
		  | updateView | Required. This method will be called when any value in the component’s property bag has changed. |
		  | getOutputs | Optional. Called by the framework prior to the receipt of new data. Use this method when dynamically managing bound properties in a control. |
		  | destroy | Required. Invoked when the component is to be removed from the DOM tree. Used for cleanup and to release any memory that the component is using. |
		- interaction
		  ![Diagram of methods through a Framework Runtime process in a standardized lifecycles.](https://learn.microsoft.com/en-us/training/modules/get-started-component-framework/media/methods.png){:height 467, :width 514}
	- Client scripting
		- high-level structure of the client scripting API object model and namespaces
		  ![](https://learn.microsoft.com/en-sg/training/modules/common-actions-client-script-power-platform/media/xrm-object.png){:height 205, :width 564}
		- TODO: https://learn.microsoft.com/en-us/training/paths/extend-power-platform-model-driven-app/
- Microsoft Dataverse extensibility
	- Using API
		- web api
		- Organization Service: sdk
	- Event pipeline 
	  ![](https://learn.microsoft.com/en-us/training/modules/introduction-power-platform-extensibility-model/media/stages.png){:height 327, :width 412}
	- Custom API
	- Microsoft Dataverse business event
	- Custom Process Actions (Custom Action)
		- define a single verb (or message)
		- doesn’t have to be associated with a specific table
		- [limitations](https://learn.microsoft.com/en-us/power-apps/developer/data-platform/business-events#custom-process-actions)
			- can be disabled in the UI
			- Until recently no way to prevent synchronous plug-in steps to be registered on custom process actions, which means anyone could register synchronous steps that could change the behavior of the custom process action or even cancel it.
	- two ways to create custom messages in dataverse: custom API and Custom Process Actions
		- [Compare Custom Process Action and Custom API](https://learn.microsoft.com/en-us/power-apps/developer/data-platform/custom-actions#compare-custom-process-action-and-custom-api)
	- Workflows/Power Automate flows vs. plugins
	  | Capability | Power Automate Flow | Workflow | Plugin |
	  | ---- | ---- | ---- |
	  | Synchronous or Asynchronous | Asynchronous | Either (Power Automate flows are recommended instead of asynchronous workflows) | Either |
	  | Access External Data | Yes, using connectors | No | Yes, using APIs, some security restrictions |
	  | Maintenance | Makers | Business Users | Developers |
	  | Can Run As | Current user or flow owner | Current user or workflow owner | Any licensed user, system, or current user |
	  | Can Run On Demand | Yes | Yes | No |
	  | Can Nest Child Processes | Yes | Yes | Yes |
	  | Execution Stage | After | Before/After | Before/After |
	  | Triggers | Create, Column Change, Delete, On Demand, Scheduled | Create, Column Change, Delete, On Demand | Create, Column Change, Delete, other messages including custom |
- [Community tools for Microsoft Dataverse](https://learn.microsoft.com/en-us/power-apps/developer/data-platform/community-tools)