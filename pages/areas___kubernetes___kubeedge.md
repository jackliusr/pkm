- ![](https://raw.githubusercontent.com/kubeedge/kubeedge/master/docs/images/kubeedge_arch.png){:height 611, :width 742}
- architecture
	- [EdgeD](https://kubeedge.io/docs/architecture/edge/edged): an edge node module which manages pod lifecycle
	- EventBus: acts as an interface for sending/receiving messages on mqtt topics
	- Edge hub: responsible for interacting with CloudHub component present in the cloud. It can connect to the CloudHub using either a web-socket connection or using [QUIC](https://quicwg.org/ops-drafts/draft-ietf-quic-applicability.html) protocol. It supports functions like sync cloud side resources update, report edged side host and device status changes.
	- DeviceTwin
	- MetaManager: the message processor between edged and edgehub. It's also responsible for storing/retrieving metadata to/from a lightweight database(SQLite).
	- ServiceBus: an HTTP client to interact with HTTP servers (REST), offering HTTP client capabilities to components of the cloud to reach HTTP servers running at the edge.
- [EdgeMesh](https://edgemesh.netlify.app/)
	- Edge Gateway: Edge Gateway provides the ability to access the internal services of the cluster through the gateway
	- ![](https://edgemesh.netlify.app/images/guide/em-ig.png){:height 354, :width 671}
	-
- beehive: Pluggable module(in-process microservice) and cross-module communication Framework
- Device Manager
- mapper: an application that is used to connect and control devices
	- [bluetooth mapper](https://kubeedge.io/docs/developer/mappers/bluetooth)
	- [modbus mapper](https://kubeedge.io/docs/developer/mappers/modbus)
	- Opcua mapper
- **[SLSA requirements and compliance](https://kubeedge.io/blog/reach-slsa-l3#how-kubeedge-reaches-slsa-3)**
	- <table><thead><tr><th><strong>Requirement</strong></th><th><strong>L1</strong></th><th><strong>L2</strong></th><th><strong>L3</strong></th><th><strong>L4</strong></th></tr></thead><tbody><tr><td><strong>Source</strong></td><td></td><td></td><td></td><td></td></tr><tr><td>Version  controlled</td><td></td><td>Y</td><td>Y</td><td>Y</td></tr><tr><td>Verified  history</td><td></td><td></td><td>Y</td><td>Y</td></tr><tr><td>Retained  indefinitely</td><td></td><td></td><td>Y</td><td>Y</td></tr><tr><td>Two-person  reviewed</td><td></td><td></td><td></td><td>Y</td></tr><tr><td><strong>Build</strong></td><td></td><td></td><td></td><td></td></tr><tr><td>Scripted  build</td><td>Y</td><td>Y</td><td>Y</td><td>Y</td></tr><tr><td>Build service</td><td></td><td>Y</td><td>Y</td><td>Y</td></tr><tr><td>Build as code</td><td></td><td></td><td>Y</td><td>Y</td></tr><tr><td>Ephemeral  environment</td><td></td><td></td><td>Y</td><td>Y</td></tr><tr><td>Isolated</td><td></td><td></td><td>Y</td><td>Y</td></tr><tr><td>Parameterless</td><td></td><td></td><td></td><td>Y</td></tr><tr><td>Hermetic</td><td></td><td></td><td></td><td>Y</td></tr><tr><td><strong>Provenance</strong></td><td></td><td></td><td></td><td></td></tr><tr><td>Available</td><td>Y</td><td>Y</td><td>Y</td><td>To-do</td></tr><tr><td>Authenticated</td><td></td><td>Y</td><td>Y</td><td>To-do</td></tr><tr><td>Service  generated</td><td></td><td>Y</td><td>Y</td><td>To-do</td></tr><tr><td>Non-falsifiable</td><td></td><td></td><td>Y</td><td>To-do</td></tr><tr><td>Dependencies  complete</td><td></td><td></td><td></td><td>To-do</td></tr><tr><td><strong>Common</strong></td><td></td><td></td><td></td><td></td></tr><tr><td>Security</td><td></td><td></td><td></td><td>Y</td></tr><tr><td>Access</td><td></td><td></td><td></td><td>Y</td></tr><tr><td>Superusers</td><td></td><td></td><td></td><td>Y</td></tr></tbody></table>