- login flow
	- terraform login
	  logseq.order-list-type:: number
	- [Generate a token](https://developer.hashicorp.com/terraform/tutorials/cloud/cloud-login#generate-a-token)
	  logseq.order-list-type:: number
	- copy the token to cli
	  logseq.order-list-type:: number
- migrate state to cloud
	- Configure Terraform Cloud integration
	  ``` hcl
	  terraform {
	    cloud {
	      organization = "ORGANIZATION-NAME"
	      workspaces {
	        name = "learn-terraform-cloud-migrate"
	      }
	  }
	  ```
	- authenticate with terraform cloud
	- Migrate the state file: terraform init
	- Configure the Terraform Cloud workspace:
- /home/jackliusr/.terraform.d/credentials.tfrc.json
  
  ``` json
  {
    "credentials": {
      "app.terraform.io": {
        "token": "F2aaIh5eOhAYcc.atlasv1.7775NOPEzo82qN88elI0qgbcyu3Jr0N4rluUqzIHEgsNf5uRxPfJ7DiV3QzwEXoNOPE"
      }
    }
  }
  ```
- run triggers: Terraform Cloud's run triggers allow you to link workspaces so that a successful apply in a source workspace will queue a run in the workspace linked to it with a run trigger
- Terraform Cloud agents: The agent polls Terraform Cloud or Terraform Enterprise for any changes to your configuration and executes the changes locally, so you do not need to allow public ingress traffic to your resources
- Terraform Cloud Kubernetes Operator
  ![](https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dtutorials%26version%3Dmain%26asset%3Dpublic%252Fimg%252Fterraform%252Fkubernetes%252Foperator%252Ftfc-operator-k8s-diagram.png%26width%3D950%26height%3D494&w=1920&q=75){:height 489, :width 859}
- Variable sets: avoid redefining the same variables across workspaces