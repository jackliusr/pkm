- building block
- components
- apps vs components targets
- Diagrid Conductor
	- App Visualizer
	- Advisor
	- Certificate Rotation and Management
	- Cost Optimization
- fault tolerance resiliency policies
	- Timeouts
	- Retries/back-offs
	- Circuit breakers
- actor
	- Actor reminders: a mechanism to trigger `persistent` callbacks on an actor at specified times. Their functionality is similar to timers. But unlike timers, reminders are triggered under all circumstances until the actor explicitly unregisters them or the actor is explicitly deleted or the number in invocations is exhausted. Specifically, reminders are triggered across actor deactivations and failovers because the Dapr actor runtime persists the information about the actors’ reminders using Dapr actor state provider.
	- Actor timers
- | Actors | Workflows |
  | ---- | ---- | ---- |
  | Actors can interact with the sidecar using either HTTP or gRPC. | Workflows only use gRPC. Due to the workflow gRPC protocol’s complexity, an SDK is *required* when implementing workflows. |
  | Actor operations are pushed to application code from the sidecar. This requires the application to listen on a particular *app port*. | For workflows, operations are *pulled* from the sidecar by the application using a streaming protocol. The application doesn’t need to listen on any ports to run workflows. |
  | Actors explicitly register themselves with the sidecar. | Workflows do not register themselves with the sidecar. The embedded engine doesn’t keep track of workflow types. This responsibility is instead delegated to the workflow application and its SDK. |