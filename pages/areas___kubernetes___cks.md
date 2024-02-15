- [how to scheduler exams](https://trainingportal.linuxfoundation.org/learn/dashboard)
- topics and weight:
  | DOMAIN | WEIGHT |
  | ---- | ---- | ---- |
  | Cluster Setup | 10% |
  | Cluster Hardening | 15% |
  | System Hardening | 15% |
  | Minimize Microservice Vulnerabilities | 20% |
  | Supply Chain Security | 20% |
  | Monitoring, Logging, and Runtime Security | 20% |
- [Security](https://kubernetes.io/docs/concepts/security/)
- [Certified Kubernetes Security Specialist (CKS) - V1.26](https://github.com/leandrocostam/cks-preparation-guide)
- 云原生|kubernetes|2022年底cks真题解析（1-10) [link](https://blog.csdn.net/alwaysbefine/article/details/128689488)
  collapsed:: true
	- kube-bench 修复不安全项:
	  logseq.order-list-type:: number
	  
	  ``` 
	  Context
	  针对 kubeadm 创建的 cluster 运行 CIS 基准测试工具时，发现了多个必须立即解决的问题。
	  Task
	  通过配置修复所有问题并重新启动受影响的组件以确保新的设置生效。
	  修复针对 API 服务器发现的所有以下违规行为：
	  1.2.7 Ensure that the --authorization-mode argument is not set to AlwaysAllow FAIL 
	  1.2.8 Ensure that the --authorization-mode argument includes Node FAIL 
	  1.2.9 Ensure that the --authorization-mode argument includes RBAC FAIL 
	  1.2.18 Ensure that the --insecure-bind-address argument is not set FAIL （1.25 中这项题目没给出，但最好也检查一下，模拟环境里需要
	  改）
	  1.2.19 Ensure that the --insecure-port argument is set to 0 FAIL （1.25 中这项题目没给出，不需要再修改了）
	  修复针对 kubelet 发现的所有以下违规行为：
	  Fix all of the following violations that were found against the kubelet:
	  4.2.1 Ensure that the anonymous-auth argument is set to false FAIL
	  4.2.2 Ensure that the --authorization-mode argument is not set to AlwaysAllow FAIL
	  注意：尽可能使用 Webhook 身份验证/授权。
	  修复针对 etcd 发现的所有以下违规行为：
	  Fix all of the following violations that were found against etcd:
	  2.2 Ensure that the --client-cert-auth argument is set to true FAIL
	  ```
	  
	  ``` bash
	  kube-bench -c 4.2.2
	  ```
	- Pod 指定 ServiceAccount
	  logseq.order-list-type:: number
	  
	  ``` markdown
	  # Context
	  您组织的安全策略包括：
	  . ServiceAccount 不得自动挂载 API 凭据
	  . ServiceAccount 名称必须以“-sa”结尾
	  清单文件 /cks/sa/pod1.yaml 中指定的 Pod 由于 ServiceAccount 指定错误而无法调度。
	  请完成一下项目：
	  # Task
	  1. 在现有 namespace qa 中创建一个名为 backend-sa 的新 ServiceAccount，
	  确保此 ServiceAccount 不自动挂载 API 凭据。
	  2. 使用 /cks/sa/pod1.yaml 中的清单文件来创建一个 Pod。
	  3. 最后，清理 namespace qa 中任何未使用的 ServiceAccount
	  ```
	  
	  ``` yaml
	  apiVersion: v1
	  kind: ServiceAccount
	  metadata:
	   name: backend-sa #修改 name
	   namespace: qa #注意添加 namespace
	  automountServiceAccountToken: false #修改为 false，表示不自动挂载 secre
	  ```
	  
	  ``` bash
	  查看所有 sa
	  kubectl get sa -n qa
	  查看已经在用的 sa
	  kubectl get pod -n qa -o yaml | grep -i serviceAccountName
	  删除不用的 sa
	  kubectl delete sa test01 -n qa
	  ```
	- RBAC - RoleBinding: **迷惑性**
	  logseq.order-list-type:: number
	  
	  ``` 
	  Context
	  绑定到 Pod 的 ServiceAccount 的 Role 授予过度宽松的权限。完成以下项目以减少权限集。
	  Task
	  一个名为 web-pod 的现有 Pod 已在 namespace db 中运行。
	  编辑绑定到 Pod 的 ServiceAccount service-account-web 的现有 Role，仅允许只对 services 类型的资源执行 get 操作。
	  在 namespace db 中创建一个名为 role-2 ，并仅允许只对 namespaces 类型的资源执行 delete 操作的新 Role。
	  创建一个名为 role-2-binding 的新 RoleBinding，将新创建的 Role 绑定到 Pod 的 ServiceAccount。
	  注意：请勿删除现有的 RoleBinding
	  ```
	- 默认网络策略
	  logseq.order-list-type:: number
	  
	  ``` 
	  Context
	  一个默认拒绝（default-deny）的 NetworkPolicy 可避免在未定义任何其他 NetworkPolicy 的 namespace 中意外公开 Pod。
	  Task
	  为所有类型为 Ingress+Egress 的流量在 namespace testing 中创建一个名为 denypolicy 的新默认拒绝 NetworkPolicy。
	  此新的 NetworkPolicy 必须拒绝 namespace testing 中的所有的 Ingress + Egress 流量。
	  将新创建的默认拒绝 NetworkPolicy 应用与在 namespace testing 中运行的所有 Pod。
	  你可以在 /cks/net/p1.yaml 找到一个模板清单文件。
	  ```
	- 网络策略 NetworkPolicy
	  logseq.order-list-type:: number
	  
	  ``` 
	  Task
	  创建一个名为 pod-restriction 的 NetworkPolicy 来限制对在 namespace dev-team 中运行的 Pod products-service 的访问。
	  只允许以下 Pod 连接到 Pod products-service
	  ⚫ namespace qaqa 中的 Pod
	  ⚫ 位于任何 namespace，带有标签 environment: testing 的 Pod
	  注意：确保应用 NetworkPolicy。
	  ```
	- 创建 Secret
	  logseq.order-list-type:: number
	  
	  ``` 
	  Task
	  在 namespace istio-system 中获取名为 db1-test 的现有 secret 的内容
	  将 username 字段存储在名为 /cks/sec/user.txt 的文件中，并将 password 字段存储在名为 /cks/sec/pass.txt 的文件中。
	  注意：你必须创建以上两个文件，他们还不存在。
	  注意：不要在以下步骤中使用/修改先前创建的文件，如果需要，可以创建新的临时文件。
	  在 istio-system namespace 中创建一个名为 db2-test 的新 secret，内容如下：
	  username : production-instance
	  password : KvLftKgs4aVH
	  最后，创建一个新的 Pod，它可以通过卷访问 secret db2-test ：
	  Pod 名称 secret-pod
	  Namespace istio-system
	  容器名 dev-container
	  镜像 nginx
	  卷名 secret-volume
	  挂载路径 /etc/secret
	  ```
	- Dockerfile 检测
	  logseq.order-list-type:: number
	  
	  ``` markdown
	  Task
	  分析和编辑给定的 Dockerfile /cks/docker/Dockerfile（基于 **ubuntu:16.04** 镜像），
	  并修复在文件中拥有的突出的安全/最佳实践问题的两个指令。
	  分析和编辑给定的清单文件 /cks/docker/deployment.yaml ，
	  并修复在文件中拥有突出的安全/最佳实践问题的两个字段。
	  注意：请勿添加或删除配置设置；只需修改现有的配置设置让以上两个配置设置都不再有安全/最佳实践问题。
	  注意：如果您需要非特权用户来执行任何项目，请使用用户 ID 65535 的用户 nobody 。
	  只修改即可，不需要创建
	  ```
		- 这一题是两个任务，第一个任务是dockerfile的安全排查，dockerfile里是镜像版本不正确，需要修改为ubuntu：16.04 还一个是USER 指定的是root，修改为**nobody**就可以了，十分简单的两个地方。
		  logseq.order-list-type:: number
		- 第二个任务是/cks/docker/deployment.yaml 文件的安全排查，一个是pod的安全上下文权限问题，一个是标签问题
		  logseq.order-list-type:: number
		- Dockerfile
		  logseq.order-list-type:: number
		  
		  ``` Dockerfile
		  <1> 修改 Dockerfile
		  vi /cks/docker/Dockerfile
		  1、仅将 CMD 上面的 USER root 修改为 USER nobody，不要改其他的
		  USER nobody
		  2、修改基础镜像为题目要求的 ubuntu:16.04
		  FROM ubuntu:16.04
		  ```
		- **/cks/docker/deployment.yaml **
		  logseq.order-list-type:: number
		  ![](https://img-blog.csdnimg.cn/1e37ec7afd9746778bbc899231662a4d.png)
		  ![](https://img-blog.csdnimg.cn/966d8064688b49238ee894e157b9a72f.png)
	- 沙箱运行容器 gVisor
	  logseq.order-list-type:: number
	  
	  ``` 
	  该 cluster 使用 containerd 作为 CRI 运行时。containerd 的默认运行时处理程序是 runc。
	  containerd 已准备好支持额外的运行时处理程序 runsc (gVisor)。
	  Task
	  使用名为 runsc 的现有运行时处理程序，创建一个名为 untrusted 的 RuntimeClass。
	  更新 namespace server 中的所有 Pod 以在 gVisor 上运行。
	  您可以在 /cks/gVisor/rc.yaml 中找到一个模版清单。
	  ```
	- AppArmor
	  logseq.order-list-type:: number
	  
	  ``` 
	  Task
	  在 cluster 的工作节点 node02 上，实施位于 /etc/apparmor.d/nginx_apparmor 的现有 APPArmor 配置文件。
	  编辑位于 /cks/KSSH00401/nginx-deploy.yaml 的现有清单文件以应用 AppArmor 配置文件。
	  最后，应用清单文件并创建其中指定的 Pod 。
	  请注意，考试时，考题里已表明 APPArmor 在工作节点上，所以你需要 ssh 到开头写的工作节点上。
	  ```
	- ImagePolicyWebhook 容器镜像扫描
	  logseq.order-list-type:: number
	  
	  ``` markdown
	  # Context
	  cluster 上设置了容器镜像扫描器，但尚未完全集成到 cluster 的配置中。
	  完成后，容器镜像扫描器应扫描并拒绝易受攻击的镜像的使用。
	  # Task
	  注意：你必须在 cluster 的 master 节点上完成整个考题，所有服务和文件都已被准备好并放置在该节点上。
	  给定一个目录 /etc/kubernetes/epconfig 中不完整的配置，
	  以及具有 HTTPS 端点 https://image-bouncer-webhook.default.svc:1323/image_policy 的功能性容器镜像扫描器：
	  1. 启用必要的插件来创建镜像策略
	  2. 校验控制配置并将其更改为隐式拒绝（implicit deny）
	  3. 编辑配置以正确指向提供的 HTTPS 端点
	  最后，通过尝试部署易受攻击的资源 /cks/img/web1.yaml 来测试配置是否有效。
	  ```
- 云原生|kubernetes|2022年底cks真题解析（11-16) [link](https://blog.csdn.net/alwaysbefine/article/details/128717226)
	- Trivy 扫描镜像安全漏洞
	  logseq.order-list-type:: number
	  
	  ``` 
	  Task
	  使用 Trivy 开源容器扫描器检测 namespace kamino 中 Pod 使用的具有严重漏洞的镜像。
	  查找具有 High 或 Critical 严重性漏洞的镜像，并删除使用这些镜像的 Pod。
	  注意：Trivy 仅安装在 cluster 的 master 节点上，
	  在工作节点上不可使用。
	  你必须切换到 cluster 的 master 节点才能使用 Trivy。
	  ```
	  
	  ```bash
	  kubectl get pods -n kamino  -o custom-columns=name:metadata.name,image:spec.containers[*].image
	  cat <<EOF | xargs -I{} sh -c "trivy -q image --severity HIGH,CRITICAL {{}} | grep -B2 'Total:'"
	  
	  EOF
	  ```
	- Container 安全上下文
	  logseq.order-list-type:: number
	  
	  ``` 
	  Context
	  Container Security Context 应在特定 namespace 中修改 Deployment。
	  Task
	  按照如下要求修改 sec-ns 命名空间里的 Deployment secdep
	  一、用 ID 为 30000 的用户启动容器（设置用户 ID 为: 30000）
	  二、不允许进程获得超出其父进程的特权（禁止 allowPrivilegeEscalation）
	  三、以只读方式加载容器的根文件系统（对根文件的只读权限）
	  ```
	  ```yaml
	  securityContext:
	      runAsUser: 30000
	      allowPrivilegeEscalation: false
	      readOnlyRootFilesystem: true
	  ```
	- 日志审计 log audit
	  logseq.order-list-type:: number
	  
	  ``` markdown
	  Task
	  在 cluster 中启用审计日志。为此，请启用日志后端，并确保：
	  ⚫ 日志存储在 /var/log/kubernetes/audit-logs.txt
	  ⚫ 日志文件能保留 10 天
	  ⚫ 最多保留 2 个旧审计日志文件
	  /etc/kubernetes/logpolicy/sample-policy.yaml 提供了基本策略。它仅指定不记录的内容。
	  注意：基本策略位于 cluster 的 master 节点上。
	  编辑和扩展基本策略以记录：
	  ⚫ RequestResponse 级别的 persistentvolumes 更改
	  ⚫ namespace front-apps 中 configmaps 更改的请求体
	  ⚫ Metadata 级别的所有 namespace 中的 ConfigMap 和 Secret 的更改
	  此外，添加一个全方位的规则以在 Metadata 级别记录所有其他请求。
	  注意：不要忘记应用修改后的策略。
	  ```
	  
	  ``` yaml
	  apiVersion: audit.k8s.io/v1
	  kind: Policy
	  rules:
	  - level: Metadata
	  ###此处省略默认带有的一些规则，不要修改，而是继续添加如下规则。
	   # namespaces changes at RequestResponse level
	  - level: RequestResponse
	    resources:
	    - group: ""
	      resources: ["persistentvolumes"] #根据题目要求修改，比如题目要求的是 namespaces。
	   #the request body of persistentvolumes/pods changes in the namespace front-apps
	  - level: Request
	    resources:
	    - group: ""
	      resources: ["configmaps"] #根据题目要求修改，比如题目要求的是 persistentvolumes 或者 pods。
	    namespaces: ["front-apps"]
	   # Log configmap and secret changes in all other namespaces at the Metadata level.
	  - level: Metadata
	    resources:
	    - group: ""
	      resources: ["secrets", "configmaps"]
	   # Also, add a catch-all rule to log all other requests at the Metadata level.
	  - level: Metadata
	    omitStages:
	    - "RequestReceived"
	  ```
	- 启用 API server 认证
	  logseq.order-list-type:: number
	  
	  ``` 
	  Context
	  由 kubeadm 创建的 cluster 的 Kubernetes API 服务器，出于测试目的，
	  临时配置允许未经身份验证和未经授权的访问，授予匿名用户 cluster-admin 的访问权限.
	  Task
	  重新配置 cluster 的 Kubernetes APl 服务器，以确保只允许经过身份验证和授权的 REST 请求。
	  使用授权模式 Node,RBAC 和准入控制器 NodeRestriction。
	  删除用户 system:anonymous 的 ClusterRoleBinding 来进行清理。
	  注意：所有 kubectl 配置环境/文件也被配置使用未经身份验证和未经授权的访问。
	  你不必更改它，但请注意，一旦完成 cluster 的安全加固， kubectl 的配置将无法工作。
	  您可以使用位于 cluster 的 master 节点上，cluster 原本的 kubectl 配置文件
	  /etc/kubernetes/admin.conf ，以确保经过身份验证的授权的请求仍然被允许。
	  
	  
	  确保只有认证并且授权过的 REST 请求才被允许
	  编辑/etc/kubernetes/manifests/kube-apiserver.yaml，修改下面内容
	  - --authorization-mode=AlwaysAllow
	  - --enable-admission-plugins=AlwaysAdmit
	  vi /etc/kubernetes/manifests/kube-apiserver.yaml
	  修改为
	  - --authorization-mode=Node,RBAC #注意，只保留 Node,RBAC 这两个，中间是英文状态下的逗号。在 1.25 考试中，这一条可能默认已经有
	  了，但还是要检查确认一下。
	  - --enable-admission-plugins=NodeRestriction #在 1.25 考试中，这一个原先为 AlwaysAdmit，需要修改为 NodeRestriction。
	  重启 kubelet
	  systemctl daemon-reload
	  systemctl restart kubelet
	  ```
	- TLS 安全配置
	  logseq.order-list-type:: number
	  
	  ``` 
	  Task
	  通过 TLS 加强 kube-apiserver 安全配置，要求
	  1、kube-apiserver 除了 VersionTLS13 及以上的版本可以使用，其他版本都不允许使用。
	  2、密码套件（Cipher suite）为 TLS_AES_128_GCM_SHA256
	  通过 TLS 加强 ETCD 安全配置，要求
	  1、密码套件（Cipher suite）为 TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
	  ```
	  no need to check doc
	  ``` bash
	  ~$ k -n kube-system exec -it kube-apiserver-kind-control-plane -- kube-apiserver --help |grep tls-
	  --cert-dir string                        The directory where the TLS certs are located. If --tls-cert-file and --tls-private-key-file are provided, this flag will be ignored. (default "/var/run/kubernetes")
	  --tls-cert-file string                   File containing the default x509 Certificate for HTTPS. (CA cert, if any, concatenated after server cert). If HTTPS serving is enabled, and --tls-cert-file and --tls-private-key-file are not provided, a self-signed certificate and key are generated for the public address and saved to the directory specified by --cert-dir.
	  --tls-cipher-suites strings              Comma-separated list of cipher suites for the server. If omitted, the default Go cipher suites will be used.
	  --tls-min-version string                 Minimum TLS version supported. Possible values: VersionTLS10, VersionTLS11, VersionTLS12, VersionTLS13
	  --tls-private-key-file string            File containing the default x509 private key matching --tls-cert-file.
	  --tls-sni-cert-key namedCertKey          A pair of x509 certificate and private key file paths, optionally suffixed with a list of domain patterns which are fully qualified domain names, possibly with prefixed wildcard segments. The domain patterns also allow IP addresses, but IPs should only be used if the apiserver has visibility to the IP address requested by a client. If no domain patterns are provided, the names of the certificate are extracted. Non-wildcard matches trump over wildcard matches, explicit domain patterns trump over extracted names. For multiple key/certificate pairs, use the --tls-sni-cert-key multiple times. Examples: "example.crt,example.key" or "foo.crt,foo.key:*.foo.com,foo.com". (default [])
	  --service-account-key-file stringArray              File containing PEM-encoded x509 RSA or ECDSA private or public keys, used to verify ServiceAccount tokens. The specified file can contain multiple keys, and the flag can be specified multiple times with different files. If unspecified, --tls-private-key-file is used. Must be specified when --service-account-signing-key-file is provided
	  
	  ~$ k -n kube-system exec -it etcd-kind-control-plane -- etcd -h | grep cipher
	     --cipher-suites '' Comma-separated list of supported TLS cipher suites between client/server and peers (empty will be auto-populated by Go).
	  ```
	- **Sysdig & falco**
	  logseq.order-list-type:: number
	  ``` 
	  Task：
	  使用运行时检测工具来检测 Pod tomcat123 单个容器中频发生成和执行的异常进程。
	  有两种工具可供使用：
	  ⚫ sysdig
	  ⚫ falco
	  注： 这些工具只预装在 cluster 的工作节点 node02 上，不在 master 节点。
	  使用工具至少分析 30 秒 ，使用过滤器检查生成和执行的进程，将事件写到 /opt/KSR00101/incidents/summary 文件中，
	  其中包含检测的事件， 格式如下：
	  timestamp,uid/username,processName
	  保持工具的原始时间戳格式不变。
	  注： 确保事件文件存储在集群的工作节点上。
	  请注意，考试时，考题里已表明 sysdig 在工作节点上，所以你需要 ssh 到开头写的工作节点上。
	  ```
		- answer
		  
		  ``` bash
		  #-M  monitor
		  # 
		  sysdig -M 30 -p "%evt.time,%user.name,%proc.name" \
		     --cri /run/containerd/containerd.sock \
		    container.name=tomcat123 >> /opt/KSR00101/incidents/summary
		  ```
- pass4success https://www.pass4success.com/linux-foundation/exam/cks
	- runtimeClass
	  ``` 
	  Context
	  
	  This cluster uses containerd as CRI runtime.
	  
	  Containerd's default runtime handler is runc. Containerd has been prepared to support an additional runtime handler, runsc (gVisor).
	  
	  Task
	  
	  Create a RuntimeClass named sandboxed using the prepared runtime handler named runsc.
	  
	  Update all Pods in the namespace server to run on gVisor.
	  ```
	- Manul Analysis
	  
	  ``` 
	  Context: Cluster:prod Master node:master1 Worker node:worker1
	  
	  You can switch the cluster/configuration context using the following command:
	  
	  [desk@cli] $kubectl config use-context prod
	  
	  Task: Analyse and edit the given Dockerfile (based on theubuntu:18:04image) 
	  /home/cert_masters/Dockerfilefixing two instructions present in the file being prominent security/best-practice issues.
	  
	  Analyse and edit the given manifest file /home/cert_masters/mydeployment.yaml 
	  fixing two fields present in the file being prominent security/best-practice issues.
	  
	  Note:Don't add or remove configuration settings; only modify the existing 
	  configuration settings, so that two configuration settings each are no longer security/best-practice concerns. 
	  Should you need an unprivileged user for any of the tasks, use usernobodywith user id65535
	  ```
	-
	-
- [Kubernetes CKS 2023 Complete Course - Theory - Practice](https://www.udemy.com/course/certified-kubernetes-security-specialist/)
  url:: https://www.udemy.com/course/certified-kubernetes-security-specialist/learn/lecture/23062478
  date:: 2023-06-4
  type:: course
	- Section 6: Cluster Setup - Network Policies
		- https://labs-map.isovalent.com/
		- editor: https://editor.networkpolicy.io/
	- Section 7: Cluster Setup - GUI Elements
	- Section 8: Cluster Setup - Secure Ingress
	- Section 9: Cluster Setup - Node Metadata Protection
	- Section 10: Cluster Setup - CIS Benchmarks
	- Section 11: Cluster Setup - Verify Platform Binaries
	- Section 12: Cluster Hardening - RBAC
	- Section 13: Cluster Hardening - Exercise caution in using ServiceAccounts
	- Section 14: Cluster Hardening - Restrict API Access
	- Section 15: Cluster Hardening - Upgrade Kubernetes
	- Section 23: Supply Chain Security - Image Vulnerability Scanning
		- Clair: an open source project for the [static analysis](https://en.wikipedia.org/wiki/Static_program_analysis) of vulnerabilities in application containers (currently including [OCI](https://github.com/opencontainers/image-spec/blob/master/spec.md) and [docker](https://github.com/docker/docker/blob/master/image/spec/v1.2.md)).
		- trivy:
	- Section 24: Supply Chain Security - Secure Supply Chain
		- image digest
		- opa whitelist registries
		- ImagePolicyWebhook
	- Section 25: Runtime Security - Behavioral Analytics at host and container level
	  collapsed:: true
		- strace
		- strace /proc on etcd
		- /proc and environment variable
		- falco [[areas/kubernetes/falco]]
	- Section 26: Runtime Security - Immutability of containers at runtime
	  collapsed:: true
		- pod & container level
		- ways:
			- image level
				- enforce: remove bash shell, make file system readonly, run as non-root
			- startupProbe: hacky
			- initContainer?
			- securityContext: mount emptyDir for writing
				- ``` yaml
				  readOnlyRootFilesystem: true
				  ```
			- RBAC: only certain persons can edit pod specs
	- Section 27: Runtime Security - [Auditing](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/)
		- Each request can be recorded with an associated *stage*. The defined stages are
			- `RequestReceived`
			- `ResponseStarted`
			- `ResponseComplete`
			- **Panic**
		- Audit policy: defines **rules** about what events should be recorded and what data they should include
			- audit level:
				- `None`
				- `Metadata`
				- `Request`
				- `RequestResponse`
		- Audit backends
			- log: [JSONlines](https://jsonlines.org/)
			- Webhook
		- [Event batching](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/#batching)
		- https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/
	- Section 28: System Hardening - Kernel Hardening Tools
		- apparmor: AppArmor is Mandatory Access Control (MAC) like security system for Linux. AppArmor confines individual programs to a set of **files, capabilities, network access and rlimits**, collectively known as the AppArmor policy for the program, or simply as a profile
			- [Securing a Pod](https://kubernetes.io/docs/tutorials/security/apparmor/#securing-a-pod)
				- annotations: 
				  ```yaml
				  container.apparmor.security.beta.kubernetes.io/<container_name>: <profile_ref>
				  ```
				- The `profile_ref` can be one of:
					- `runtime/default` to apply the runtime's default profile
					- `localhost/<profile_name>` to apply the profile loaded on the host with the name `<profile_name>`
					- `unconfined` to indicate that no profiles will be loaded
			- commands: package apparmor
				- aa-status: aa-
				- **aa-genprof / aa-logprof**
				- **aa-enforce / aa-complain**
				- **aa-disable / aa-uncomplain**
				- **aa-logprof / aa-logparser**
				- **aa-autodep**
				- **aa-mergeprof**
				- **apparmor_parser**: loads AppArmor profiles into the kernel
				- **aa-cleanprof**
		- seccomp
			- [Create a Pod that uses the container runtime default seccomp profile](https://kubernetes.io/docs/tutorials/security/seccomp/#create-a-pod-that-uses-the-container-runtime-default-seccomp-profile)
			  
			  ``` yaml
			    securityContext:
			      seccompProfile:
			        type: RuntimeDefault
			  ---
			    securityContext:
			      seccompProfile:
			        type: Localhost
			        localhostProfile: profiles/audit.json
			  ```
			-
	- Section 29: System Hardening - Reduce Attack Surface
	- Section 30: Linux Foundation Simulator Sessions
- other resources for CKS
  + [ ] [KodeKloud CKS Course by Mumshad](https://kodekloud.com/courses/certified-kubernetes-security-specialist-cks/)
  + [ ] [KodeKloud CKS Challenges](https://kodekloud.com/courses/cks-challenges/)
  + [ ] [Killer Shell](https://killer.sh/cks)
  + [ ] [KillerCoda](https://killercoda.com/killer-shell-cks)
  + [ ] [KodeKloud Kubernetes Challenges](https://kodekloud.com/courses/kubernetes-challenges/)
	- immutable pod:
		- ``` yaml
		  #remove /bin/sh, /bin/ash
		  #allowPrivilegeEscalation: false
		  #runAsUser: 0
		  ```
- first attempts: weak points
	- Monitoring, **Logging** and Runtime Security
		- https://github.com/deemoprobe/kubernetes/blob/main/Kubernetes%E9%85%8D%E7%BD%AE%E6%A1%88%E4%BE%8B.md#7-%E5%AE%A1%E8%AE%A1%E6%97%A5%E5%BF%97
		  
		  ``` markdown
		  # Task
		  Enable audit logs in the cluster.To do so, enable the log backend, and ensurethat:
		   1. logs are stored at /var/log/kubernetes/audit-logs.txt
		   2. log files are retained for 30 days
		   3. at maximum, a number of 10 auditlog files are retained
		  A basic policy is provided at /etc/kubernetes/logpolicy/sample-policy.yaml. it only specifies what not to log.
		  The base policy is located on the cluster master node.
		  Edit and extend the basic policy to log:
		   1. Cronjobs changes at RequestResponse level
		   2. the request body of persistentvolumes changes in the namespace front-apps
		   3. ConfigMap and Secret changes in all namespaces at the Metadata level
		  Also, add a catch-all ruie to log all otherrequests at the Metadata level.
		  Don not forget to apply the modifiedpolicy.
		  
		  # Prepare
		  $ kubectl config use-context KSRS00602
		  # Answer
		  $ ssh ksrs00602-master
		  $ vim /etc/kubernetes/logpolicy/sample-policy.yaml
		  apiVersion: audit.k8s.io/v1
		  kind: Policy
		  # Don't generate audit events for all requests in RequestReceived stage.
		  omitStages:
		    - "RequestReceived"
		  rules:
		    # Log pod changes at RequestResponse level
		    - level: RequestResponse
		      resources:
		      - group: ""
		        resources: ["cronjobs"]
		    # Log the request body of configmap changes in kube-system.
		    - level: Request
		      resources:
		      - group: ""
		        resources: ["persistentvolumes"]
		      namespaces: ["front-apps"]
		    # Log configmap and secret changes in all other namespaces at the Metadata level.
		    - level: Metadata
		      resources:
		      - group: ""
		        resources: ["secrets", "configmaps"]
		    # A catch-all rule to log all other requests at the Metadata level.
		    - level: Metadata
		      omitStages:
		        - "RequestReceived"
		  $ vim /etc/kubernetes/manifests/kube-apiserver.yaml
		  ...
		  spec:
		    containers:
		    - command:
		      - kube-apiserver
		      # 添加下面四行
		      - --audit-policy-file=/etc/kubernetes/logpolicy/sample-policy.yaml
		      - --audit-log-path=/var/log/kubernetes/audit-logs.txt
		      - --audit-log-maxage=30
		      - --audit-log-maxbackup=10
		      ...
		  # 重启kubelet
		  $ systemctl restart kubelet
		  # 可以查看一下日志输出，如果报错查看一下数据卷是否挂载，/etc/kubernetes/manifests/kube-apiserver.yaml文件最后
		  # 没挂载的话用参考链接中后端日志挂载数据卷并配置hostPath
		  $ tail -1 /var/log/kubernetes/audit-logs.txt
		  $ exit
		  ```
		- https://github.com/deemoprobe/kubernetes/blob/main/Kubernetes%E9%85%8D%E7%BD%AE%E6%A1%88%E4%BE%8B.md#12-imagepolicywebhook
		  
		  ``` markdown
		  # context
		  A container image scanner is set up on the cluster, but it is not yet fully integrated into the cluster configuration. When complete, the container image scanner shall scan for and reject the use of vulnerable images.
		  # Task
		  You have to complete the entire task on the cluster master node, where all services and files have been prepared and placed.
		  Given an incomplete configuration in directory /etc/kubernetes/epconfig and a functional container image scanner with HTTPS endpoint http://wakanda.local:8082/image_policy:
		  1. Enable the necessary plugins to create an image policy
		  2. Validate the control configuration and change it to an implicit deny
		  3. Edit the configuration to point t the provided HTTPS endpoint correctly.
		  Finally , test if the configuration is working by trying to deploy the vulnerable resource /root/KSSC00202/configuration-test.yaml
		  You can find the container image scanner log file at /var/log/imagepolicy/acme.log
		  
		  # Prepare
		  $ kubectl config use-context KSSC00202
		  # Answer
		  $ ssh kssc00202-master
		  $ vim /etc/kubernetes/epconfig/admission_configuration.json
		  'defaultAllow': false # 改成 false
		  $ vim /etc/kubernetes/epconfig/kubeconfig.yaml
		  apiVersion: v1
		  kind: Config
		  clusters:
		  - cluster:
		   certificate-authority: /etc/kubernetes/pki/server.crt
		   # 添加server配置
		   server: https://wakanda.local:8082/image_policy
		  ...
		  # 配置挂载，考试时一般会提前配置好
		    - mountPath: /etc/kubernetes/epconfig
		      name: epconfig
		  hostNetwork: true
		  ...
		  volumes:
		  - name: epconfig
		    hostPath:
		      path: /etc/kubernetes/epconfig
		  # 添加ImagePolicyWebhook准入控制插件以及配置文件
		  $ vim /etc/kubernetes/manifests/kube-apiserver.yaml
		  - --enable-admission-plugins=NodeRestriction,ImagePolicyWebhook
		  - --admission-control-configfile=/etc/kubernetes/epconfig/admission_configuration.json
		  $ systemctl restart kubelet
		  $ exit
		  
		  ```
	- Supply Chain Security
		- https://github.com/deemoprobe/kubernetes/blob/main/Kubernetes%E9%85%8D%E7%BD%AE%E6%A1%88%E4%BE%8B.md#9-dockerfile
		  
		  ``` markdown
		  # Task
		  Analyze and edit the given Dockerfile (based on the ubuntu:16.04 image) /home/candidate/KSSC00301/Dockerfile fixing two instructions present in the file being prominent security/best-practice issues.
		  Analyze and edit the given manifest file /home/candidate/KSSC00301/deployment.yaml fixing two fields present in the file being prominent security/best-practice issues.
		  You can use normal user(nobody),ID is 65535. 
		  
		  # Prepare
		  $ kubectl config use-context KSSC00301
		  # Answer
		  $ vim /home/candidate/KSSC00301/Dockerfile
		  # root改为nobody
		  USER nobody
		  USER nobody
		  $ vim /home/candidate/KSSC00301/deployment.yaml
		  # 对应内容True|False修改为下面两处
		  'privileged': False,'readOnlyRootFilesystem': True,
		  ```
		- trivy
		  
		  ``` bash
		  trivy -q  image nginx | grep -B2 -E "Total:"
		  nginx (debian 12.2)
		  ===================
		  Total: 134 (UNKNOWN: 0, LOW: 83, MEDIUM: 35, HIGH: 14, CRITICAL: 2)
		  ```
	- Cluster Hardening
	- https://github.com/deemoprobe/kubernetes/blob/main/Kubernetes%E9%85%8D%E7%BD%AE%E6%A1%88%E4%BE%8B.md
		- https://github.com/deemoprobe/kubernetes/blob/main/Kubernetes%E9%85%8D%E7%BD%AE%E6%A1%88%E4%BE%8B.md#2-serviceaccount
		- https://github.com/deemoprobe/kubernetes/blob/main/Kubernetes%E9%85%8D%E7%BD%AE%E6%A1%88%E4%BE%8B.md#7-%E5%AE%A1%E8%AE%A1%E6%97%A5%E5%BF%97