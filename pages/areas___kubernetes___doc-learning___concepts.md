- concepts
	- cluster architecture
	  collapsed:: true
		- node
			- [ways to have nodes added to the API server](https://kubernetes.io/docs/concepts/architecture/nodes/#management)
				- self-registration
				- manual
			- `shutdownGracePeriod`, shutdownGracePeriodCriticalPods
				- **shutdownGracePeriodByPodPriority**
			- taint: node.kubernetes.io/out-of-service:NoExecute or `node.kubernetes.io/out-of-service:NoSchedule`
		- communication between nodes and control plane
			- [API server to kubelet](https://kubernetes.io/docs/concepts/architecture/control-plane-node-communication/#api-server-to-kubelet)
				- Fetching logs for pods.
				- Attaching (usually through `kubectl`) to running pods.
				- Providing the kubelet's port-forwarding functionality.
		- controllers
			- Controller pattern
				- control via api server
				- direct control
			- Ways of running controllers
		- Leases
			- node heartbeat
			- leader election
			- api server identity
			- workloads
		- Cloud controller manager (KCCM)
			- functions: node, route, service
		- cgroup
			- Identify the cgroup version on Linux Nodes
			  ``` bash
			  stat -fc %T /sys/fs/cgroup/
			  # cgroup2fs or tmpfs
			  ```
		- CRI:
			- protocol: https://github.com/kubernetes/cri-api/blob/c75ef5b/pkg/apis/runtime/v1/api.proto
		- Garbage Collection:
		- Mixed Version Proxy:
	- containers
	  collapsed:: true
		- image:
			- `imagePullPolicy`: **IfNotPresent**, Always, Never
			- ImagePullBackOff
			- Image pull per runtime class
			- `serializeImagePulls` `maxParallelImagePulls`
			- Multi-architecture images with image indexes
		- runtimeclass
		  collapsed:: true
			- [Scheduling ](https://kubernetes.io/docs/concepts/containers/runtime-class/#scheduling)
			  If `scheduling` is not set, this RuntimeClass is assumed to be supported by all nodes.
			  
			  ``` 
			    scheduling    <Scheduling>
			      nodeSelector        <map[string]string>
			      tolerations <[]Toleration>
			        effect    <string>
			        key       <string>
			        operator  <string>
			        tolerationSeconds <integer>
			        value     <string>
			  ```
			- Pod Overhead: podFixed    <map[string]Quantity>
		- Container Lifecycle Hooks:
			- **PostStart** and **PreStop**
			- implementations: exec, httpGet, sleep
			- Hook handler execution
				- kubelet: `httpGet` , `tcpSocket` and `sleep`
				- container: exec
			- Hook handler calls are synchronous within the context of the Pod containing the Container. This means that for a **PostStart** hook, the Container ENTRYPOINT and hook fire asynchronously. However, if the hook takes too long to run or hangs, the Container cannot reach a `running` state
			- Hook delivery guarantees: at least once
	- workloads
	  collapsed:: true
		- pod
		  collapsed:: true
			- pod lifecycle
			  collapsed:: true
				- pod phase:
					- .status: Pending, Running, Succeeded, Failed, Unknown
				- container state: Running, Waiting, Terminated
				- `restartPolicy`: OnFailure, Always
					- After containers in a Pod exit, the kubelet restarts them with an **exponential back-off delay** (**10s**, 20s,40s, …), that is capped at **five minutes**. Once a container has executed for **10 minutes** without any problems, the kubelet resets the restart backoff timer for that container
				- Pod readiness
					- ContainersReady
				- `PodReadyToStartContainers`
				- conainer probes:
					- check mechanisms: exec, grpc, httpGet, tcpSocket
					- livenessProbe, readinessProbe, startupProbe
				- Termination of Pods:
					- If the `preStop` hook is still running after the grace period expires, the kubelet requests a small, one-off grace period extension of 2 seconds.
					- Garbage collection of Pods: PodGC
			- init containers and sidecar containers
			- Disruptions
				- Voluntary and involuntary disruptions
				- Pod disruption budgets
				- Pod disruption conditions: `DisruptionTarget` and reasons
				- Separating Cluster Owner and Application Owner Roles
			- Ephemeral Containers:
				- not supported by [static pods](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/).
				- ```bash
				  kubectl run ephemeral-demo --image=registry.k8s.io/pause:3.1 --restart=Never
				  kubectl debug -it ephemeral-demo --image=busybox:1.28 --target=ephemeral-demo
				  ```
			- Pod Quality of Service Classes
				- Guaranteed: all containers must have both requests and limits for memory and cpu,  requests must be equal to limits
				- `Burstable`: At least one Container in the Pod has a memory or CPU request or limit.
				- BestEffort
			- User namespaces: a Linux feature that allows to map users in the container to different users in the host. Furthermore, the capabilities granted to a pod in a user namespace are valid only in the namespace and void outside of it.
				- idmap
				- pod.spec.hostUsers
				- Integration with Pod security admission checks
				- Limitations: hostNetwork, hostIPC, hostPID
			- Downward API: allows containers to consume information about themselves or the cluster without using the Kubernetes client or API server.
				- two ways:
					- as [environment variables](https://kubernetes.io/docs/tasks/inject-data-application/environment-variable-expose-pod-information/)
					- as [files in a `downwardAPI` volume](https://kubernetes.io/docs/tasks/inject-data-application/downward-api-volume-expose-pod-information/)
				- `fieldRef` and `resourceFieldRef`
		- Workload Management:
			- deployment
				- Rollover (aka multiple updates in-flight)
			- replicaset
				- Non-Template Pod acquisitions
				- [Deleting just a ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/#deleting-just-a-replicaset): --cascade=orphan
				- Pod deletion cost:
					- annotation, [`controller.kubernetes.io/pod-deletion-cost`](https://kubernetes.io/docs/reference/labels-annotations-taints/#pod-deletion-cost)
					- range: [-2147483648, 2147483647].
			- statefulset
				- Pod Identity
				- Ordinal Index: annotation: apps.kubernetes.io/pod-index
				- Start ordinal: .spec.ordinals.start
				- Deployment and Scaling Guarantees
			- daemonset
				- Communicating with Daemon Pods
					- Push
					- NodeIP  and known port
					- DNS
					- Service
				- Alternatives to DaemonSet
			- job
			  collapsed:: true
				- .spec.parallelism
				- .spec.completions
				- .spec.completionMode: Indexed, `NonIndexed`
				- `backoffLimitPerIndex`
				- .spec.podFailurePolicy: handle Pod failures based on the container exit codes and the Pod conditions.
				  
				  ``` yaml
				    podFailurePolicy:
				      rules:
				      - action: FailJob
				        onExitCodes:
				          containerName: main      # optional
				          operator: In             # one of: In, NotIn
				          values: [42]
				      - action: Ignore             # one of: Ignore, FailJob, Count
				        onPodConditions:
				        - type: DisruptionTarget   # indicates Pod disruption
				  ```
				- `activeDeadlineSeconds`
				- [TTL mechanism for finished Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/#ttl-mechanism-for-finished-jobs): `.spec.ttlSecondsAfterFinished`
				- job patterns: 
				  <table><thead><tr><th>Pattern</th><th style="text-align:center"><code>.spec.completions</code></th><th style="text-align:center"><code>.spec.parallelism</code></th></tr></thead><tbody><tr><td><a href="/docs/tasks/job/coarse-parallel-processing-work-queue/">Queue with Pod Per Work Item</a></td><td style="text-align:center">W</td><td style="text-align:center">any</td></tr><tr><td><a href="/docs/tasks/job/fine-parallel-processing-work-queue/">Queue with Variable Pod Count</a></td><td style="text-align:center">null</td><td style="text-align:center">any</td></tr><tr><td><a href="/docs/tasks/job/indexed-parallel-processing-static/">Indexed Job with Static Work Assignment</a></td><td style="text-align:center">W</td><td style="text-align:center">any</td></tr><tr><td><a href="/docs/tasks/job/job-with-pod-to-pod-communication/">Job with Pod-to-Pod Communication</a></td><td style="text-align:center">W</td><td style="text-align:center">W</td></tr><tr><td><a href="/docs/tasks/job/parallel-processing-expansion/">Job Template Expansion</a></td><td style="text-align:center">1</td><td style="text-align:center">should be 1</td></tr></tbody></table>
				- advanced usage:
					- Suspending a Job:
						- `.spec.suspend`:
						- When a Job is resumed from suspension, its `.status.startTime` field will be reset to the current time. This means that the `.spec.activeDeadlineSeconds` timer will be stopped and reset when a Job is suspended and resumed.
					- Specifying your own Pod selector
						- `.spec.selector`
						- `manualSelector: true`
					- Elastic Indexed Jobs: mutating both `.spec.parallelism` and `.spec.completions` together such that `.spec.parallelism == .spec.completions`.
					- `podReplacementPolicy`
			- cronjob
				- Deadline for delayed Job start: `startingDeadlineSeconds`
				- `concurrencyPolicy`: Allow, Forbid, Replace
				- .spec.timeZone
				- [Cannot determine if job needs to be started: Too many missed start time (> 100). Set or decrease .spec.startingDeadlineSeconds or check clock skew](https://stackoverflow.com/questions/60540032/cannot-determine-if-job-needs-to-be-started-too-many-missed-start-time-100)
			- ReplicationController
				- Isolating pods from a ReplicationController: changing their labels
	- Services, Load Balancing, and Networking
	  collapsed:: true
		- network model: four concerns:
		  collapsed:: true
			- pods can communicate with all other pods on any other [node](https://kubernetes.io/docs/concepts/architecture/nodes/) without NAT
			- agents on a node (e.g. system daemons, kubelet) can communicate with all pods on that node
		- Service
		  collapsed:: true
			- Services without selectors
				- manual creation of EndpointSlice
				- ExternalName
			- Over-capacity endpoints: the 1000 backing endpoint limit only affects the legacy Endpoints API
				- [`endpoints.kubernetes.io/over-capacity: truncated`](https://kubernetes.io/docs/reference/labels-annotations-taints/#endpoints-kubernetes-io-over-capacity)
			- Headless Services
			- sessionAffinity
			- External IPs: When network traffic arrives into the cluster, with the external IP (as destination IP) and the port matching that Service, rules and routes that Kubernetes has configured ensure that the traffic is routed to one of the endpoints for that Service.
		- Ingress
		  collapsed:: true
			- Resource backends
			- DefaultBackend
		- Ingress Controllers
		- Gateway API
		- EndpointSlices
		- Network Policies
		  collapsed:: true
			- NetworkPolicy and   `hostNetwork`   pods
			- **What you can't do with network policies (at least, not yet)**
			- NetworkPolicy's impact on existing connections
		- DNS for Services and Pods
		  collapsed:: true
			- Services
				- my-svc.my-namespace.svc.cluster-domain.example
				- Headless Services: resolves to the set of IPs of all of the Pods selected by the Service. Clients are expected to consume the set or else use standard round-robin selection from the set.
				- SRV records: _port-name._port-protocol.my-svc.my-namespace.svc.cluster-domain.example
			- Pods:
				- `pod-ipv4-address.my-namespace.pod.cluster-domain.example`. 172-17-0-3.default.pod.cluster.local
				- `hostname` `subdomain`
				- setHostnameAsFQDN
		- IPv4/IPv6 dual-stack
		  collapsed:: true
			- [Switching Services between single-stack and dual-stack ](https://kubernetes.io/docs/concepts/services-networking/dual-stack/#switching-services-between-single-stack-and-dual-stack)
			- Egress traffic
				- transparent proxying vs IP masquerading
				- not routable addresses: Private IPv6 addresses can be divided into ==site-local and link-local addresses==:
					- Site-local addresses: Have the scope of an entire site or organization
					- Link-local addresses: Uniquely identify hosts on a single network link. They have a prefix of FE80 and can only be used for communication on the local network. Link-local addresses are not routable and do not appear within the routing table as destinations
		- Topology Aware Routing
		  collapsed:: true
			- annotation:
			  
			  ``` yaml
			  annotations:
			    service.kubernetes.io/topology-mode: Auto
			  ```
			- When it works best:
				- Incoming traffic is evenly distributed
				- The Service has 3 or more endpoints per zone
			- how it works
				- EndpointSlice controller
				  
				  ``` yaml
				  apiVersion: discovery.k8s.io/v1
				  kind: EndpointSlice
				  metadata:
				    name: example-hints
				    labels:
				      kubernetes.io/service-name: example-svc
				  addressType: IPv4
				  ports:
				    - name: http
				      protocol: TCP
				      port: 80
				  endpoints:
				    - addresses:
				        - "10.1.2.3"
				      conditions:
				        ready: true
				      hostname: pod-1
				      zone: zone-a
				      hints:
				        forZones:
				          - name: "zone-a"
				  ```
				- kube-proxy
			- safeguards
			- constraints
		- Networking on Windows
		- Service ClusterIP allocation:
			- The allocation strategy implemented in Kubernetes to allocate ClusterIPs to Services reduces the risk of collision.
			- The `ClusterIP` range is divided, based on the formula `min(max(16, cidrSize / 16), 256)`, described as *never less than 16 or more than 256 with a graduated step between them*.
			- Dynamic IP assignment uses the upper band by default, once this has been exhausted it will use the lower range. This will allow users to use static allocations on the lower band with a low risk of collision.
		- Service Internal Traffic Policy
			- *Service Internal Traffic Policy* enables internal traffic restrictions to only route internal traffic to endpoints **within the node** the traffic originated from. The "internal" traffic here refers to traffic originated from Pods in the current cluster.
			- **internalTrafficPolicy**: Local
	- storage
	  collapsed:: true
		- volumes
		  collapsed:: true
			- hostPath types: 
			  <table><thead><tr><th style="text-align:left">Value</th><th style="text-align:left">Behavior</th></tr></thead><tbody><tr><td style="text-align:left"><code>‌""</code></td><td style="text-align:left">Empty string (default) is for backward compatibility, which means that no checks will be performed before mounting the <code>hostPath</code> volume.</td></tr><tr><td style="text-align:left"><code>DirectoryOrCreate</code></td><td style="text-align:left">If nothing exists at the given path, an empty directory will be created there as needed with permission set to 0755, having the same group and ownership with Kubelet.</td></tr><tr><td style="text-align:left"><code>Directory</code></td><td style="text-align:left">A directory must exist at the given path</td></tr><tr><td style="text-align:left"><code>FileOrCreate</code></td><td style="text-align:left">If nothing exists at the given path, an empty file will be created there as needed with permission set to 0644, having the same group and ownership with Kubelet.</td></tr><tr><td style="text-align:left"><code>File</code></td><td style="text-align:left">A file must exist at the given path</td></tr><tr><td style="text-align:left"><code>Socket</code></td><td style="text-align:left">A UNIX socket must exist at the given path</td></tr><tr><td style="text-align:left"><code>CharDevice</code></td><td style="text-align:left"><em>(Linux nodes only)</em> A character device must exist at the given path</td></tr><tr><td style="text-align:left"><code>BlockDevice</code></td><td style="text-align:left"><em>(Linux nodes only)</em> A block device must exist at the given path</td></tr></tbody></table>
			- subPath and subPathExpr: Use the `subPathExpr` field to construct `subPath` directory names from downward API environment variables. The `subPath` and `subPathExpr` properties are mutually exclusive.
			- `csi` volume
				- A `csi` volume can be used in a Pod in three different ways:
					- through a reference to a [PersistentVolumeClaim](https://kubernetes.io/docs/concepts/storage/volumes/#persistentvolumeclaim)
					- with a [generic ephemeral volume](https://kubernetes.io/docs/concepts/storage/ephemeral-volumes/#generic-ephemeral-volumes)
					- with a [CSI ephemeral volume](https://kubernetes.io/docs/concepts/storage/ephemeral-volumes/#csi-ephemeral-volumes) if the driver supports that
				- fields: driver, volumeHandle, readOnly, fsType, volumeAttributes, controllerPublishSecretRef, nodeExpandSecretRef, nodePublishSecretRef, nodeStageSecretRef
		- Persistent Volumes
			- **dataSource** and `dataSourceRef`:: Unlike the `dataSource` field, which can only contain either a reference to another PersistentVolumeClaim or to a VolumeSnapshot, the `dataSourceRef` field can contain a reference to any object in the same namespace, except for core objects other than PVCs
			- Cross namespace data sources
			- volume-data-source-validator: Controller responsible for validating PVC data sources
			- Writing Portable Configuration: PersistentVolumeClaim
		- Projected Volumes
		  collapsed:: true
			- types
				- [`secret`](https://kubernetes.io/docs/concepts/storage/volumes/#secret)
				- [`downwardAPI`](https://kubernetes.io/docs/concepts/storage/volumes/#downwardapi)
				- [`configMap`](https://kubernetes.io/docs/concepts/storage/volumes/#configmap)
				- [`serviceAccountToken`](https://kubernetes.io/docs/concepts/storage/projected-volumes/#serviceaccounttoken)
				- [`clusterTrustBundle`](https://kubernetes.io/docs/concepts/storage/projected-volumes/#clustertrustbundle)
					- ``` yaml
					    volumes:
					    - name: token-vol
					      projected:
					        sources:
					        - clusterTrustBundle:
					            name: example
					            path: example-roots.pem
					        - clusterTrustBundle:
					            signerName: "example.com/mysigner"
					            labelSelector:
					              matchLabels:
					                version: live
					            path: mysigner-roots.pem
					            optional: true
					  ```
			- SecurityContext interactions
		- Ephemeral Volumes
		  collapsed:: true
			- Types of ephemeral volumes
				- [emptyDir](https://kubernetes.io/docs/concepts/storage/volumes/#emptydir): empty at Pod startup, with storage coming locally from the kubelet base directory (usually the root disk) or RAM
				- [configMap](https://kubernetes.io/docs/concepts/storage/volumes/#configmap), [downwardAPI](https://kubernetes.io/docs/concepts/storage/volumes/#downwardapi), [secret](https://kubernetes.io/docs/concepts/storage/volumes/#secret): inject different kinds of Kubernetes data into a Pod
				- [CSI ephemeral volumes](https://kubernetes.io/docs/concepts/storage/ephemeral-volumes/#csi-ephemeral-volumes): similar to the previous volume kinds, but provided by special [CSI](https://kubernetes.io/docs/concepts/storage/volumes/#csi) drivers which specifically [support this feature](https://kubernetes-csi.github.io/docs/ephemeral-local-volumes.html)
				- [generic ephemeral volumes](https://kubernetes.io/docs/concepts/storage/ephemeral-volumes/#generic-ephemeral-volumes), which can be provided by all storage drivers that also support persistent volumes
			- [local ephemeral storage](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#local-ephemeral-storage)
			- PersistentVolumeClaim naming: Naming of the automatically created PVCs is deterministic: the name is a combination of the Pod name and volume name, with a hyphen (`-`) in the middle.  The deterministic naming also introduces a potential conflict between different Pods
		- Storage Classes
		  collapsed:: true
			- Allowed topologies
			  
			  ``` yaml
			  allowedTopologies:
			  - matchLabelExpressions:
			    - key: topology.kubernetes.io/zone
			      values:
			      - us-central-1a
			      - us-central-1b
			  ```
		- Volume Attributes Classes
		  collapsed:: true
			- VolumeAttributesClass
			  
			  ``` yaml
			  apiVersion: storage.k8s.io/v1alpha1
			  kind: VolumeAttributesClass
			  metadata:
			    name: silver
			  driverName: pd.csi.storage.gke.io
			  parameters:
			    provisioned-iops: "3000"
			    provisioned-throughput: "50" 
			  ```
			- external-provisioner
			- external-resizer
		- Dynamic Volume Provisioning
		- Volume Snapshots
		  collapsed:: true
			- `VolumeSnapshotContent`
			- `VolumeSnapshot`
			- `VolumeSnapshotClass`
			- `sourceVolumeMode`
		- Volume Snapshot Classes
			- provides a way to describe the "classes" of storage when provisioning a volume snapshot
			- driver, deletionPolicy, parameters
		- CSI Volume Cloning
		- Storage Capacity
			- [CSIStorageCapacity ](https://kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/csi-storage-capacity-v1/#CSIStorageCapacity)
			- [`CSIDriverSpec.StorageCapacity` field](https://kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/csi-driver-v1/#CSIDriverSpec):
		- Node-specific Volume Limits
			- [Kubernetes default limits](https://kubernetes.io/docs/concepts/storage/storage-limits/#kubernetes-default-limits)
			- Custom limits
			- [Dynamic volume limits](https://kubernetes.io/docs/concepts/storage/storage-limits/#dynamic-volume-limits)
		- Volume Health Monitoring
			- External Health Monitor controller
		- Windows Storage
	- configuration
	  collapsed:: true
		- Configuration Best Practices
			- Create a [Service](https://kubernetes.io/docs/concepts/services-networking/service/) before its corresponding backend workloads (Deployments or ReplicaSets), and before any workloads that need to access it. When Kubernetes starts a container, it provides environment variables pointing to all the Services which were running when the container was started.
		- configmaps
			- `binaryData`
			- `immutable`: can only delete and recreate the ConfigMap. Because existing Pods maintain a mount point to the deleted ConfigMap, it is recommended to recreate these pods
		- Secrets
		  collapsed:: true
			- alternative:
			- Types of Secret
			  <table><thead><tr><th>Built-in Type</th><th>Usage</th></tr></thead><tbody><tr><td><code>Opaque</code></td><td>arbitrary user-defined data</td></tr><tr><td><code>kubernetes.io/service-account-token</code></td><td>ServiceAccount token</td></tr><tr><td><code>kubernetes.io/dockercfg</code></td><td>serialized <code>~/.dockercfg</code> file</td></tr><tr><td><code>kubernetes.io/dockerconfigjson</code></td><td>serialized <code>~/.docker/config.json</code> file</td></tr><tr><td><code>kubernetes.io/basic-auth</code></td><td>credentials for basic authentication</td></tr><tr><td><code>kubernetes.io/ssh-auth</code></td><td>credentials for SSH authentication</td></tr><tr><td><code>kubernetes.io/tls</code></td><td>data for a TLS client or server</td></tr><tr><td><code>bootstrap.kubernetes.io/token</code></td><td>bootstrap token data</td></tr></tbody></table>
			- immutable
			- Configure least-privilege access to Secrets
			  
			  ``` yaml
			  annotions:
			     kubernetes.io/enforce-mountable-secrets: "true".
			  ```
		- resources:
		  collapsed:: true
			- cpu, memory,` hugepages-<size>`, ephemeral-storage
			- Local ephemeral storage: ephemeral data that comes from running Pods: logs, and `emptyDir` volumes. [node-level container logs](https://kubernetes.io/docs/concepts/cluster-administration/logging/#logging-at-the-node-level)
				- two ways to configure local ephemeral storage on a node
					- single file system
					- two file system
				- [Ephemeral storage consumption management ](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#resource-emphemeralstorage-consumption)
					- ways to measure Pod storage use: Periodic scanning, filesystem Project quotas
						- Kubernetes uses project IDs starting from `1048576`
				- **Extended resources**
		- Organizing Cluster Access Using kubeconfig Files
		  collapsed:: true
			- `KUBECONFIG`, --kubeconfig, $HOME/.kube/config, --context
			- proxy: configure `kubectl` to use a proxy per cluster using `proxy-url` in your kubeconfig file
			  
			  ``` yaml
			  apiVersion: v1
			  kind: Config
			  
			  clusters:
			  - cluster:
			      proxy-url: http://proxy.example.org:3128
			      server: https://k8s.example.org/k8s/clusters/c-xxyyzz
			    name: development
			  
			  users:
			  - name: developer
			  
			  contexts:
			  - context:
			    name: development
			  
			  ```
		- Resource Management for Windows nodes
			- job object
	- security
	  collapsed:: true
		- Overview of Cloud Native Security: 4C
		  ![](https://kubernetes.io/images/docs/4c.png)
		- Pod Security Standards
		  collapsed:: true
			- <table><thead><tr><th>Profile</th><th>Description</th></tr></thead><tbody><tr><td><strong style="white-space:nowrap">Privileged</strong></td><td>Unrestricted policy, providing the widest possible level of permissions. This policy allows for known privilege escalations.</td></tr><tr><td><strong style="white-space:nowrap">Baseline</strong></td><td>Minimally restrictive policy which prevents known privilege escalations. Allows the default (minimally specified) Pod configuration.</td></tr><tr><td><strong style="white-space:nowrap">Restricted</strong></td><td>Heavily restricted policy, following current Pod hardening best practices.</td></tr></tbody></table>
			- Alternatives [](https://kubernetes.io/docs/concepts/security/pod-security-standards/#alternatives)
		- Service Accounts
			- Authenticating service account credentials
			- alternative
		- Pod Security Admission
		  collapsed:: true
			- modes
			  <table><caption style="display:none">Pod Security Admission modes</caption><thead><tr><th style="text-align:left">Mode</th><th style="text-align:left">Description</th></tr></thead><tbody><tr><td style="text-align:left"><strong>enforce</strong></td><td style="text-align:left">Policy violations will cause the pod to be rejected.</td></tr><tr><td style="text-align:left"><strong>audit</strong></td><td style="text-align:left">Policy violations will trigger the addition of an audit annotation to the event recorded in the <a href="/docs/tasks/debug/debug-cluster/audit/">audit log</a>, but are otherwise allowed.</td></tr><tr><td style="text-align:left"><strong>warn</strong></td><td style="text-align:left">Policy violations will trigger a user-facing warning, but are otherwise allowed.</td></tr></tbody></table>
			- ``` yaml
			  # The per-mode level label indicates which policy level to apply for the mode.
			  #
			  # MODE must be one of `enforce`, `audit`, or `warn`.
			  # LEVEL must be one of `privileged`, `baseline`, or `restricted`.
			  pod-security.kubernetes.io/<MODE>: <LEVEL>
			  
			  # Optional: per-mode version label that can be used to pin the policy to the
			  # version that shipped with a given Kubernetes minor version (for example v1.29).
			  #
			  # MODE must be one of `enforce`, `audit`, or `warn`.
			  # VERSION must be a valid Kubernetes minor version, or `latest`.
			  pod-security.kubernetes.io/<MODE>-version: <VERSION>
			  ```
			- Exemptions
		- Security For Windows Nodes
			- RunAsUserName vs RunAsUser
			- ContainerUser vs `ContainerAdministrator`
		- Controlling Access to the Kubernetes API
		  collapsed:: true
			- <img src="https://kubernetes.io/images/docs/admin/access-control-overview.svg"></img>
			- Policy, SubjectAccessReview
		- Role Based Access Control Good Practices
		  collapsed:: true
			- User impersonation
			- Kubernetes RBAC - privilege escalation risks
				- [Listing secrets](https://kubernetes.io/docs/concepts/security/rbac-good-practices/#listing-secrets)
				- [Workload creation](https://kubernetes.io/docs/concepts/security/rbac-good-practices/#workload-creation)
				- [Persistent volume creation](https://kubernetes.io/docs/concepts/security/rbac-good-practices/#persistent-volume-creation)
				- [Access to `proxy` subresource of Nodes](https://kubernetes.io/docs/concepts/security/rbac-good-practices/#access-to-proxy-subresource-of-nodes)
				- [Escalate verb](https://kubernetes.io/docs/concepts/security/rbac-good-practices/#escalate-verb)
				- [Bind verb](https://kubernetes.io/docs/concepts/security/rbac-good-practices/#bind-verb)
				- [Impersonate verb](https://kubernetes.io/docs/concepts/security/rbac-good-practices/#impersonate-verb)
				- [CSRs and certificate issuing](https://kubernetes.io/docs/concepts/security/rbac-good-practices/#csrs-and-certificate-issuing)
				- [Token request](https://kubernetes.io/docs/concepts/security/rbac-good-practices/#token-request)
				- [Control admission webhooks](https://kubernetes.io/docs/concepts/security/rbac-good-practices/#control-admission-webhooks)
		- **Good practices for Kubernetes Secrets**
		- **Multi-tenancy**
		- Hardening Guide - Authentication Mechanisms
		- Kubernetes API Server Bypass Risks
		- Security Checklist
	- policy
	  collapsed:: true
		- using API objects, admission controllers, ValidatingAdmissionPolicy, dynamic admission control, flexible policy engines
		- LimitRange 
		  
		  ``` yaml
		  apiVersion: v1
		  kind: LimitRange
		  metadata:
		    name: cpu-resource-constraint
		  spec:
		    limits:
		    - default: # this section defines default limits
		        cpu: 500m
		      defaultRequest: # this section defines default requests
		        cpu: 500m
		      max: # max and min define the limit range
		        cpu: "1"
		      min:
		        cpu: 100m
		      type: Container
		  ```
		- Resource Quotas
		  collapsed:: true
			- compute,
			- Storage Resource
			- object count
			- quota scope:
				- scopes: 
				  <table><thead><tr><th>Scope</th><th>Description</th></tr></thead><tbody><tr><td><code>Terminating</code></td><td>Match pods where <code>.spec.activeDeadlineSeconds &gt;= 0</code></td></tr><tr><td><code>NotTerminating</code></td><td>Match pods where <code>.spec.activeDeadlineSeconds is nil</code></td></tr><tr><td><code>BestEffort</code></td><td>Match pods that have best effort quality of service.</td></tr><tr><td><code>NotBestEffort</code></td><td>Match pods that do not have best effort quality of service.</td></tr><tr><td><code>PriorityClass</code></td><td>Match pods that references the specified <a href="/docs/concepts/scheduling-eviction/pod-priority-preemption">priority class</a>.</td></tr><tr><td><code>CrossNamespacePodAffinity</code></td><td>Match pods that have cross-namespace pod <a href="/docs/concepts/scheduling-eviction/assign-pod-node">(anti)affinity terms</a>.</td></tr></tbody></table>
				- Resource Quota Per PriorityClass
				- Cross-namespace Pod Affinity Quota
		- Process ID Limits And Reservations
		- Node Resource Managers:
	- scheduling, preempting and eviction
	  collapsed:: true
		- kube-scheduler
		  collapsed:: true
			- 2 operations: filtering and scoring
			- config:
				- scheduling policies: configure *Predicates* for filtering and *Priorities* for scoring.
				- scheduling profiles: configure Plugins that implement different scheduling stages, including: `QueueSort`, `Filter`, `Score`, `Bind`, `Reserve`, `Permit`, and others. You can also configure the kube-scheduler to run different profiles
		- Assigning Pods to Nodes
		  collapsed:: true
			- Node isolation/restriction
			- *topology spread constraints*
		- Pod Overhead
		  collapsed:: true
			- Configuring Pod overhead
			  
			  ``` yaml
			  apiVersion: node.k8s.io/v1
			  kind: RuntimeClass
			  metadata:
			    name: kata-fc
			  handler: kata-fc
			  overhead:
			    podFixed:
			      memory: "120Mi"
			      cpu: "250m"
			  ```
			- Verify Pod cgroup limits
			  
			  ``` bash
			  
			  # Run this on the node where the Pod is scheduled
			  POD_ID="$(sudo crictl pods --name test-pod -q)"
			  
			  # Run this on the node where the Pod is scheduled
			  sudo crictl inspectp -o=json $POD_ID | grep cgroupsPath
			    "cgroupsPath": "/kubepods/podd7f4b509-cf94-4951-9417-d1087c92a5b2/7ccf55aee35dd16aca4189c952d83487297f3cd760f1bbf09620e206e7d0c27a"
			  
			  # Run this on the node where the Pod is scheduled.
			  # Also, change the name of the cgroup to match the cgroup allocated for your pod.
			   cat /sys/fs/cgroup/memory/kubepods/podd7f4b509-cf94-4951-9417-d1087c92a5b2/memory.limit_in_bytes
			  
			  ```
		- Pod Scheduling Readiness
		  collapsed:: true
			- `schedulingGates`
			  ```mermaid
			  stateDiagram-v2
			  
			      s1: pod created
			      s2: pod scheduling gated
			      s3: pod scheduling ready
			      s4: pod running
			      if: empty scheduling gates?
			      [*] --> s1
			      s1 --> if
			      s2 --> if: scheduling gate removed
			      if --> s2: no
			      if --> s3: yes  
			      s3 --> s4
			      s4 --> [*]
			  
			  classDef k8s fill:#326ce5,stroke:#fff,stroke-width:4px,color:#fff;
			  class s1,s2,s3,s4,if k8s
			  
			  ```
			- Mutable Pod Scheduling Directives
		- Pod Topology Spread Constraints
		  collapsed:: true
			- **skew**: Pods number matched  in current topology  - min pods matched in a topology
			- [PodTopologySpread](https://kubernetes.io/blog/2020/05/introducing-podtopologyspread/)
			- ``` yaml
			  apiVersion: v1
			  kind: Pod
			  metadata:
			    name: example-pod
			  spec:
			    # Configure a topology spread constraint
			    topologySpreadConstraints:
			      - maxSkew: <integer>
			        minDomains: <integer> # optional; beta since v1.25
			        topologyKey: <string>
			        whenUnsatisfiable: <string>
			        labelSelector: <object>
			        matchLabelKeys: <list> # optional; beta since v1.27
			        nodeAffinityPolicy: [Honor|Ignore] # optional; beta since v1.26
			        nodeTaintsPolicy: [Honor|Ignore] # optional; beta since v1.26
			  ```
			- Interaction with node affinity and node selectors: The scheduler will skip the non-matching nodes from the skew calculations if the incoming Pod has `spec.nodeSelector` or `spec.affinity.nodeAffinity` defined
			- Implicit conventions
			- Cluster-level default constraints
			  
			  ``` yaml
			  apiVersion: kubescheduler.config.k8s.io/v1beta3
			  kind: KubeSchedulerConfiguration
			  
			  profiles:
			    - schedulerName: default-scheduler
			      pluginConfig:
			        - name: PodTopologySpread
			          args:
			            defaultConstraints:
			              - maxSkew: 1
			                topologyKey: topology.kubernetes.io/zone
			                whenUnsatisfiable: ScheduleAnyway
			            defaultingType: List
			  ```
			- Built-in default constraints
			  
			  ``` yaml
			  defaultConstraints:
			    - maxSkew: 3
			      topologyKey: "kubernetes.io/hostname"
			      whenUnsatisfiable: ScheduleAnyway
			    - maxSkew: 5
			      topologyKey: "topology.kubernetes.io/zone"
			      whenUnsatisfiable: ScheduleAnyway
			  ```
			- Known limitations:
		- Taints and Tolerations
		  collapsed:: true
			- Taint based Evictions
		- Scheduling Framework
		  collapsed:: true
			- ![](https://kubernetes.io/images/docs/scheduling-framework-extensions.png){:height 397, :width 686}
		- Dynamic Resource Allocation
		  collapsed:: true
			- types:
				- **ResourceClass**
				- **ResourceClaim**
				- **ResourceClaimTemplate**
				- **PodSchedulingContext**
		- Scheduler Performance Tuning
		  collapsed:: true
			- `percentageOfNodesToScore`: also a hardcoded minimum value of 50 nodes.
			- Default threshold
			- How the scheduler iterates over Nodes: iterates over the nodes in a round robin fashion
		- Resource Bin Packing
		  collapsed:: true
			- `NodeResourcesFit` plugin
			- strategy
				- `MostAllocated`: scores the nodes based on the utilization of resources, favoring the ones with higher allocation. For each resource type, you can set a weight to modify its influence in the node score.
				- `RequestedToCapacityRatio` allows the users to specify the resources along with weights for each resource to score nodes based on the request to capacity ratio. This allows users to bin pack extended resources by using appropriate parameters to improve the utilization of scarce resources in large clusters
					- Tuning the score function: `shape` is used to specify the behavior of the `RequestedToCapacityRatio` function
					  
					  ``` yaml
					  shape:
					    - utilization: 0
					      score: 0
					    - utilization: 100
					      score: 10
					  ```
					- Node scoring for capacity allocation
		- Pod Priority and Preemption
		  collapsed:: true
			- PriorityClass: `globalDefault`, description
			- pod: .spec.priorityClassName
			- Non-preempting PriorityClass: preemptionPolicy: Never
				- scheduler back-off: if the scheduler tries these pods and they cannot be scheduled, they will be retried with lower frequency, allowing other pods with lower priority to be scheduled before them.
			- Pod priority.
				- [Effect of Pod priority on scheduling order](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/#effect-of-pod-priority-on-scheduling-order)
			- Preemption
				- `nominatedNodeName`
			- Limitations of preemption
				- Graceful termination of preemption victims
				- [PodDisruptionBudget is supported, but not guaranteed ](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/#poddisruptionbudget-is-supported-but-not-guaranteed)
				- Inter-Pod affinity on lower-priority Pods
				- Cross node preemption
				- Troubleshooting
				- Interactions between Pod priority and quality of service
		- Node-pressure Eviction: the process by which the [kubelet](https://kubernetes.io/docs/reference/generated/kubelet) proactively terminates pods to reclaim resources on nodes.
		  collapsed:: true
			- Eviction signals and thresholds
				- Soft eviction thresholds
					- eviction-soft, eviction-soft-grace-period, eviction-max-pod-grace-period
				- Hard eviction thresholds: no grace period
			- Eviction monitoring interval: housekeeping-interval, default 10
			- Node condition
			  collapsed:: true
				- <table><thead><tr><th>Node Condition</th><th>Eviction Signal</th><th>Description</th></tr></thead><tbody><tr><td><code>MemoryPressure</code></td><td><code>memory.available</code></td><td>Available memory on the node has satisfied an eviction threshold</td></tr><tr><td><code>DiskPressure</code></td><td><code>nodefs.available</code>, <code>nodefs.inodesFree</code>, <code>imagefs.available</code>, or <code>imagefs.inodesFree</code></td><td>Available disk space and inodes on either the node's root filesystem or image filesystem has satisfied an eviction threshold</td></tr><tr><td><code>PIDPressure</code></td><td><code>pid.available</code></td><td>Available processes identifiers on the (Linux) node has fallen below an eviction threshold</td></tr></tbody></table>
				- Node condition oscillation: eviction-pressure-transition-period, default 5m
				- [Reclaiming node level resources](https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/#reclaim-node-resources)
				- Pod selection for kubelet eviction
					- determine the pod eviction order:
						- Whether the pod's resource usage exceeds requests
						- [Pod Priority](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)
						- The pod's resource usage relative to requests
					- ranks and evicts pods in the following order:
						- `BestEffort` or `Burstable` pods where the usage exceeds requests. These pods are evicted based on their Priority and then by how much their usage level exceeds the request.
						- `Guaranteed` pods and `Burstable` pods where the usage is less than requests are evicted last, based on their Priority.
				- Minimum eviction reclaim: --eviction-minimum-reclaim
			- Node out of memory behavior
				- The kubelet sets an `oom_score_adj` value for each container based on the QoS for the pod.
				- <table><thead><tr><th>Quality of Service</th><th><code>oom_score_adj</code></th></tr></thead><tbody><tr><td><code>Guaranteed</code></td><td>-997</td></tr><tr><td><code>BestEffort</code></td><td>1000</td></tr><tr><td><code>Burstable</code></td><td><em>min(max(2, 1000 - (1000 × memoryRequestBytes) / machineMemoryCapacityBytes), 999)</em></td></tr></tbody></table>
			- Good practices
				- [Schedulable resources and eviction policies](https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/#schedulable-resources-and-eviction-policies)
				- DaemonSets and node-pressure eviction
			- Known issues
				- --kernel-memcg-notification
				- active_file memory is not considered as available memory
			-
		- API-initiated Eviction
		  collapsed:: true
			- ``` yaml
			  {
			    "apiVersion": "policy/v1",
			    "kind": "Eviction",
			    "metadata": {
			      "name": "quux",
			      "namespace": "default"
			    }
			  }
			  ```
			- or
			  ``` bash
			  curl -v -H 'Content-type: application/json' https://your-cluster-api-endpoint.example/api/v1/namespaces/default/pods/quux/eviction -d @eviction.json
			  
			  ```
	- Cluster Administration
	  collapsed:: true
		- certificate
		- *CRI logging format*
		- Cluster-level logging architectures
			- [Using a node logging agent](https://kubernetes.io/docs/concepts/cluster-administration/logging/#using-a-node-logging-agent)
			- [Using a sidecar container with the logging agent](https://kubernetes.io/docs/concepts/cluster-administration/logging/#sidecar-container-with-logging-agent)
			- [Exposing logs directly from the application](https://kubernetes.io/docs/concepts/cluster-administration/logging/#exposing-logs-directly-from-the-application)
		- Metrics For Kubernetes System Components
			- Metric lifecycle: Alpha metric → Stable metric → Deprecated metric → Hidden metric → Deleted metric
			- show-hidden-metrics-for-version
			- Metric cardinality enforcement: --allow-label-value
		- system log
			- Log query
			  
			  ``` bash
			  kubectl get --raw "/api/v1/nodes/node-1.example/proxy/logs/?query=kubelet"
			  
			  ```
		- Traces For Kubernetes System Components
		- Proxies in Kubernetes
		- API Priority and Fairness
		  collapsed:: true
			- --max-requests-inflight and --max-mutating-requests-inflight
			- Some requests classified as "long-running"—such as remote command execution or log tailing—are not subject to the API Priority and Fairness filter. API Priority and Fairness *does* apply to **watch** requests.
			- *FlowSchemas*,
			- priority levels: The concurrency limits of the priority levels are periodically adjusted, allowing under-utilized priority levels to temporarily lend concurrency to heavily-utilized levels.
			- concepts
				- [Seats Occupied by a Request](https://kubernetes.io/docs/concepts/cluster-administration/flow-control/#seats-occupied-by-a-request)
				- [Priority Levels](https://kubernetes.io/docs/concepts/cluster-administration/flow-control/#priority-levels)
				- [Seats Occupied by a Request](https://kubernetes.io/docs/concepts/cluster-administration/flow-control/#seats-occupied-by-a-request)
				- [Execution time tweaks for watch requests](https://kubernetes.io/docs/concepts/cluster-administration/flow-control/#execution-time-tweaks-for-watch-requests)
				- [Queuing](https://kubernetes.io/docs/concepts/cluster-administration/flow-control/#queuing)
				- [Exempt requests](https://kubernetes.io/docs/concepts/cluster-administration/flow-control/#exempt-requests)
			- Resources
				- [PriorityLevelConfiguration ](https://kubernetes.io/docs/concepts/cluster-administration/flow-control/#prioritylevelconfiguration): represents a single priority level. Each PriorityLevelConfiguration has an independent limit on the number of outstanding requests, and limitations on the number of queued requests.
					- nominal concurrency limit
				- FlowSchema: A FlowSchema matches some inbound requests and assigns them to a priority level. Every inbound request is tested against FlowSchemas, starting with those with the numerically lowest `matchingPrecedence` and working upward. The first match wins.
		- Installing Addons
	- Windows in Kubernetes
	- Extending Kubernetes
	  collapsed:: true
		- Extension patterns: controller, webhook, binary plugin
		- Kubernetes extension points
		  ![](https://kubernetes.io/docs/concepts/extend-kubernetes/extension-points.png){:height 504, :width 255}
		- Compute, Storage, and Networking Extensions
			- Network Plugins
			- Device Plugins
		- Extending the Kubernetes API
			- Custom Resources,
				- Custom Controller
				- API server aggregation: The [aggregation layer](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/apiserver-aggregation/) allows you to provide specialized implementations for your custom resources by writing and deploying your own API server. The main API server delegates requests to your API server for the custom resources that you handle, making them available to all of its clients
			- Kubernetes API Aggregation Layer
				- *APIService*
				- apiserver-builder
			- Operator pattern