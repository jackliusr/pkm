- Release Cycles: Kubernetes Release Cycle
- ![](https://danielmangum.com/static/k8s-asa-caching-4.png){:height 433, :width 575}
- [The Evolution of Distributed Systems on Kubernetes](https://www.infoq.com/articles/distributed-systems-kubernetes) #inbox
- next: edge, multiple cluster, IoT, AI
- Durable Functions: Semantics for Stateful Serverles
- Kubernetes scalability envelope. 
  ![](https://storage.googleapis.com/gweb-cloudblog-publish/images/The_Kubernetes_scalability_envelope.max-600x600.jpg){:height 392, :width 566}
- Distribution Memory Usage
  | Distribution | Used |
  | Base OS, no Kubernetes | 167MB |
  | K0s | 658MB |
  | K3s | 750MB |
  | MicroK8s | 685MB |
  | MicroK8s (no HA) | 526MB |
  | Docker | 216MB |
- bare metal vs edge
- clusters
	- [[areas/kubernetes/vcluster]]
	- ocm
	- karmada
- Structured Authentication Config:
	- advantanges:
		- A new kube-apiserver flag that passes the link to the authentication configuration file;
		- Dynamic application of a configuration file after it has been modified;
		- Simultaneous use of multiple OIDC providers;
		- CEL support;
		- Rules for token validation;
		- Rules for retrieving information from a token and applying it to user attributes;
		- Structured configuration, i.e. you can use regular versioning instead of messing around with many flags.
- host os: [Fedora CoreOS](https://docs.fedoraproject.org/en-US/fedora-coreos/), [Ubuntu Core](https://ubuntu.com/core), [openSUSE MicroOS](https://microos.opensuse.org/), and [Bottlerocket OS](https://github.com/bottlerocket-os/bottlerocket)
- feature gates
	- componets: . Use `-h` flag to see a full set of feature gates for all components. To set feature gates for a component, such as kubelet, use the `--feature-gates` flag assigned to a list of feature pairs:
	- enable 
	  ``` yaml
	  # api server
	  --feature-gates=VolumeSnapshotDataSource=true
	  ```
	- check enabled feature gates: 
	  ``` bash
	  kubectl get --raw /metrics |grep kubernetes_feature_enabled
	  ```