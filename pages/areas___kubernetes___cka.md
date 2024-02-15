- load image into k8s
- [How to issue a certificate for a user](https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/#normal-user)
	- set credential https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/#add-to-kubeconfig
	  
	  ``` bash
	  kubectl config set-credentials USER_NAME  \
	  --client-certificate= \
	  --client-key= \
	  --embed-certs=true
	  ```
	- create role
	  ``` bash
	  kubectl create role pod-reader --verb=get --verb=list --verb=watch --resource=pods -n acme
	  ```
	- create role binding
	  
	  ``` bash
	  kubectl create rolebinding bob-admin-binding --clusterrole=admin --user=bob --namespace=acme
	  ```
	- How to issue a certificate for a user #card
	  card-last-interval:: 382.52
	  card-repeats:: 6
	  card-ease-factor:: 3.1
	  card-next-schedule:: 2025-01-04T04:20:22.937Z
	  card-last-reviewed:: 2023-12-18T16:20:22.937Z
	  card-last-score:: 5
	  collapsed:: true
		- [Create private key](https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/#create-private-key)
		- [Create a CertificateSigningRequest](https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/#create-certificatessigningrequest)
		- [Approve the CertificateSigningRequest](https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/#approve-certificate-signing-request)
		- [Get the certificate](https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/#get-the-certificate)
		- [Create Role and RoleBinding](https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/#create-role-and-rolebinding)
		- [Add to kubeconfig](https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/#add-to-kubeconfig)
	- Create a CertificateSigningRequest #card
	  card-last-interval:: 382.52
	  card-repeats:: 6
	  card-ease-factor:: 3.1
	  card-next-schedule:: 2025-01-04T04:20:30.515Z
	  card-last-reviewed:: 2023-12-18T16:20:30.515Z
	  card-last-score:: 5
	  collapsed:: true
		- ``` bash
		  cat <<EOF | kubectl apply -f -
		  apiVersion: certificates.k8s.io/v1
		  kind: CertificateSigningRequest
		  metadata:
		    name: myuser
		  spec:
		    request: $(cat myuser.csr | base64 | tr -d "\n")
		    signerName: kubernetes.io/kube-apiserver-client
		    expirationSeconds: 86400  # one day
		    usages:
		    - client auth
		  EOF
		  ```
	- Get the certificate #card
	  card-last-interval:: 382.52
	  card-repeats:: 6
	  card-ease-factor:: 3.1
	  card-next-schedule:: 2025-01-04T04:20:37.546Z
	  card-last-reviewed:: 2023-12-18T16:20:37.546Z
	  card-last-score:: 5
		- ``` bash
		  kubectl get csr myuser -o jsonpath='{.status.certificate}'| base64 -d > myuser.crt
		  ```
	- Create private key #card
	  card-last-interval:: 382.52
	  card-repeats:: 6
	  card-ease-factor:: 3.1
	  card-next-schedule:: 2025-01-04T04:20:42.820Z
	  card-last-reviewed:: 2023-12-18T16:20:42.821Z
	  card-last-score:: 5
		- ``` bash
		  openssl genrsa -out myuser.key 2048
		  openssl req -new -key myuser.key -out myuser.csr
		  ```
- [Create a pod using PVC](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#create-a-persistentvolumeclaim) #card
  card-last-interval:: 382.52
  card-repeats:: 6
  card-ease-factor:: 3.1
  card-next-schedule:: 2025-01-04T04:20:46.150Z
  card-last-reviewed:: 2023-12-18T16:20:46.151Z
  card-last-score:: 5
	- ``` yaml
	  apiVersion: v1
	  kind: Pod
	  metadata:
	    name: task-pv-pod
	  spec:
	    volumes:
	      - name: task-pv-storage
	        persistentVolumeClaim:
	          claimName: task-pv-claim
	    containers:
	      - name: task-pv-container
	        image: nginx
	        ports:
	          - containerPort: 80
	            name: "http-server"
	        volumeMounts:
	          - mountPath: "/usr/share/nginx/html"
	            name: task-pv-storage
	  ```
- https://killercoda.com/fa1ca33f-72b8-46e3-bca7-b3d1395472be
	- https://killercoda.com/fa1ca33f-72b8-46e3-bca7-b3d1395472be/scenario/kubernetes-cka-part2
- query-table:: true