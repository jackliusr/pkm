- commands:
	- Main commands:
	  init          Prepare your working directory for other commands
	  validate      Check whether the configuration is valid
	  plan          Show changes required by the current configuration
	  apply         Create or update infrastructure
	  destroy       Destroy previously-created infrastructure
	- All other commands:
	  console       Try Terraform expressions at an interactive command prompt
	  fmt           Reformat your configuration in the standard style
	  force-unlock  Release a stuck lock on the current workspace
	  get           Install or upgrade remote Terraform modules
	  **graph**         Generate a Graphviz graph of the steps in an operation
	  **import**        Associate existing infrastructure with a Terraform resource
	  login         Obtain and save credentials for a remote host
	  logout        Remove locally-stored credentials for a remote host
	  metadata      Metadata related commands
	  output        Show output values from your root module
	  providers     Show the providers required for this configuration
	  **refresh**       Update the state to match remote systems
	  show          Show the current state or a saved plan
	  state         Advanced state management
	  taint         Mark a resource instance as not fully functional
	  untaint       Remove the 'tainted' state from a resource instance
	  version       Show the current Terraform version
	  workspace     Workspace management
- protect secrets
	- sensitive variables: still plain text in state file
	- Automatically encrypt state at rest by storing it in Terraform cloud.
	- [Inject secrets into Terraform using the Vault provider](https://developer.hashicorp.com/terraform/tutorials/secrets/secrets-vault)
- [Top 50 Terraform Interview Questions and Answers for 2023](https://www.projectpro.io/article/terraform-interview-questions-and-answers/850)
- tools
	- terragrunt: a thin wrapper that provides extra tools for keeping your configurations DRY, working with multiple Terraform modules, and managing remote state.
	- tfsec: Security scanner for your Terraform code
	- tfmask: Terraform utility to mask select output from `terraform plan` and `terraform apply`