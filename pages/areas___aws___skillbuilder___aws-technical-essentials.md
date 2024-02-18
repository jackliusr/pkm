- global infrastructure
  collapsed:: true
	- region consideration: latency, price, service availability, and compliance.
	- Availability Zone: consists of one or more data centers with redundant power, networking, and connectivity
	- **Scope of AWS services**:  Zone, Region, or Global level
	- edge locations
- interacting with aws: AWS Management Console, AWS Command Line Interface (AWS CLI), or AWS SDKs.
- shared responsibility model
  ![](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1708156800/li4dFK1LBCSRpf-w5P021g/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/G7jsXz1OeUet0P4d_VQj8P7tpf4Xy4mAS.png){:height 326, :width 750}
- **AWS root user**
- IAM: user, role, group, policy
- compute
  collapsed:: true
	- options: vm, containers and serverless
	  ![](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1708156800/li4dFK1LBCSRpf-w5P021g/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/IbjD_sYNXMGG29wp_yamf8JnTg88tNiAQ.jpg)
	- ec2
		- AMI, location
		- instance type: family, attribute, size
		- instance lifecycle
		  ![](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1708156800/li4dFK1LBCSRpf-w5P021g/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/Xiqo31wijGzxUHcs_W-vfLyAzzrKyOEwn.png)
		- user data script
	- container service:
	  collapsed:: true
		- orchestration services:
			- Elastic Container Service (ECS): task
			  collapsed:: true
			  ![](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1708156800/li4dFK1LBCSRpf-w5P021g/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/j7c1On-84HBvzs8I_fBTShP26hpLTwZKE.png)
				- ECS container agent
				  ![](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1708156800/li4dFK1LBCSRpf-w5P021g/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/XbD8apMKo5wCAHO6_YiX8p1udFI_1rzlu.jpg)
			- eks
	- **serverless**
	  collapsed:: true
		- Fargate: for container
		- lambda
			- function,
			- trigger
			- event
			- application environment
			- deployment package
			- runtime
			- lambda function handler
- networking
  collapsed:: true
	- vpc
	  collapsed:: true
		- ![](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1708156800/li4dFK1LBCSRpf-w5P021g/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/zFbgStDJuiU7O9Qe_OaaDyPzF7zr1lKW9.png)
		- **Reserved IPs** ![](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1708156800/li4dFK1LBCSRpf-w5P021g/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/yVvxJRoMUxkJyMC6_Octk-lV6RnrruL3M.png)
			- internet gateway, virtual private gateway, direct connect
	- vpc routing
		- main route table
		- custom route table
	- vpc security
		- network access control list (network ACL):
		- security group: stateful
			- design pattern is to organize resources into different groups and create security groups for each to control network communication between them.
- storage
  collapsed:: true
	- category: file storage, block storage, and object storage
	- file storage:
		- EFS:
			- storage class
				- standard, standard IA
				- one zone, one zone IA
		- FSx: Lustre, NetApp ONTAP, OpenZFS, and Windows File Server.
	- block storage:
		- **EC2 instance store**
		- esb
			- **EBS volume types**: solid-state drives (SSDs) and hard-disk drives (HDDs).
	- object storage: s3
		- bucket, name, key, policy( iam, bucket), encryption, version, storage class, **Versioning states**
		- **lifecycle**: lifecycle configuration
- database
  collapsed:: true
	- **unmanaged and managed databases**
	- Amazon RDS
		- **Commercial:** Oracle, SQL Server
		- **Open source:** MySQL, PostgreSQL, MariaDB
		- **Cloud native: **Aurora
	- instance, storage, security, backup options, redundancy with multi-AZ
	- **Purpose-built databases**
		- **DynamoDB**: table, item, attribute
		- **ElastiCache** ( redis, memcache)
		- **DocumentDB**
		- **Keyspaces** (**Cassandra**)
		- **Neptune** (graph)
		- **Timestream**:
		- **Quantum Ledger Database**
- monitoring
  collapsed:: true
	- CloudWatch
		- free: a rate of 1 data point per metric per 5-minute interval
		- detailed monitoring: fee
		- Metrics
		- Custom metrics
		- dashboard
		- logs: group, stream, event
		- alert
- Solution Optimisation
  collapsed:: true
	- **automated monitoring, failure detection, and failover mechanisms.**
	- type of availability: active-passive or active-active.
- Traffic Routing with Elastic Load Balancing
  collapsed:: true
	- type: Application Load Balancer (ALB), Network Load Balancer (NLB), and Gateway Load Balancer (GLB)
	- ![](https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1708178400/v9ReuH4wx0nUAByHcyohAQ/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/9Nhe4XPfwf7BcJAR_edbUVOAV1agybbQ-.png){:height 516, :width 691}
- EC2 Auto Scaling
	- **Auto Scaling groups**
	- **Scaling policies**: simple, step, and target tracking scaling
- Amazon CodeWhisperer