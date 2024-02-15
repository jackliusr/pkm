- a powerful, modular, extensible platform for Kubernetes multi-cluster orchestration
- concepts:
	- **Hub Cluster**: Indicating the cluster that runs the multi-cluster control plane of OCM. Generally the hub cluster is supposed to be a light-weight Kubernetes cluster hosting merely a few fundamental controllers and services.
	- **Klusterlet**: Indicating the clusters that being managed by the hub cluster. Klusterlet might also be called “managed cluster” or “spoke cluster”. The klusterlet is supposed to actively **pulling** the latest prescriptions from the hub cluster and consistently reconciles the physical Kubernetes cluster to the expected state.
	- Architecture
	  ![](https://github.com/open-cluster-management-io/OCM/raw/main/assets/ocm-arch.png)
	- ClusterClaim
	- Add-ons and Integrations
	  collapsed:: true
		- [multicloud-operators-subscription](https://github.com/open-cluster-management-io/multicloud-operators-subscription#multicloud-operators-subscription)
			- ![](https://raw.githubusercontent.com/open-cluster-management-io/multicloud-operators-subscription/main/images/architecture.png){:height 479, :width 826}
		- Cluster proxy: an OCM addon providing L4 network connectivity from hub cluster to the managed clusters without **any additional requirement** to the managed cluster’s network infrastructure by leveraging the Kubernetes official SIG sub-project [apiserver-network-proxy](https://github.com/kubernetes-sigs/apiserver-network-proxy).
		  ![](https://open-cluster-management.io/cluster-proxy-architecture.png){:height 579, :width 769}
		- Policy framework: The policy framework provides governance capabilities to OCM managed Kubernetes clusters. Policies provide visibility and drive remediation for various security and configuration aspects to help IT administrators meet their requirements.
		  ![](https://open-cluster-management.io/policy-framework-architecture-diagram.png){:height 943, :width 760}
		- [Managed Service Account](https://github.com/open-cluster-management-io/managed-serviceaccount#managed-service-account): "Managed Service Account" is an OCM addon developed over [addon-framework](https://github.com/open-cluster-management-io/addon-framework) for synchronizing [ServiceAccount](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/) to the managed clusters and collecting the tokens from these local service accounts as secret resources back to the hub cluster.