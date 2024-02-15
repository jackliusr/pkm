- Virtual clusters are fully working Kubernetes clusters that run on top of other Kubernetes clusters. Compared to fully separate "real" clusters, virtual clusters reuse worker nodes and networking of the host cluster. used most widely in pre-production environments to reduce the total number of physical Kubernetes servers an organization needs to deploy
- architecture
  ![](https://www.vcluster.com/docs/media/diagrams/vcluster-architecture.svg){:height 350, :width 810}
- components: By default, vClusters run as a single pod (scheduled by a StatefulSet) that consists of 2 containers:
	- [**Control Plane**](https://www.vcluster.com/docs/architecture/control_plane/)
	- [**Syncer**](https://www.vcluster.com/docs/architecture/syncer/) What makes a vCluster virtual is the fact that it does not have actual worker nodes or network. Instead, it uses a so-called syncer which copies the pods that are created within the vCluster to the underlying host cluster. Then, the host cluster will actually schedule the pod and the vCluster will keep the vCluster pod and host cluster pod in sync.
- cost:
  ![](https://raw.githubusercontent.com/loft-sh/vcluster/main/docs/static/media/vcluster-comparison.png)