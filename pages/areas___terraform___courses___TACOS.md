- **T**erraform **A**utomation and **CO**laboration **S**oftware: TACOS externalize common platform-level tasks. Complex, production-grade terraform code bases will often require TACOS support
- tool:
	- Terragrunt
	- Atlantis
	- Scalr
	- Env0
	- Spacelift
	- <table>
	  <thead>
	  <tr>
	  <th>Capability/Tool</th>
	  <th>terraform Cloud</th>
	  <th>terraform Enterprise</th>
	  <th>Scalr</th>
	  <th>Env0</th>
	  <th>Spacelift</th>
	  </tr>
	  </thead>
	  <tbody>
	  <tr>
	  <td>Compliance</td>
	  <td>ISO 27001, SOC 2</td>
	  <td>ISO 27001, SOC 2</td>
	  <td>❓</td>
	  <td>SOC 2</td>
	  <td>ISO 27001, SOC 2</td>
	  </tr>
	  <tr>
	  <td>GitLab Integration</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  </tr>
	  <tr>
	  <td>Hosting</td>
	  <td>SaaS</td>
	  <td>SaaS, On-Prem</td>
	  <td>SaaS, On-Prem</td>
	  <td>SaaS</td>
	  <td>SaaS</td>
	  </tr>
	  <tr>
	  <td>Policy as Code</td>
	  <td>Sentinel</td>
	  <td>Sentinel</td>
	  <td>OPA</td>
	  <td>OPA</td>
	  <td>OPA</td>
	  </tr>
	  <tr>
	  <td>Pricing Model</td>
	  <td>Unpredictable in highers tiers</td>
	  <td>Still figuring it out</td>
	  <td>Mixed</td>
	  <td>Mixed</td>
	  <td>Per capabilities and users</td>
	  </tr>
	  <tr>
	  <td>Private Agents</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  </tr>
	  <tr>
	  <td>Private Module Registry</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅ - with CI/CD</td>
	  </tr>
	  <tr>
	  <td>RBAC</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✔️ - hierarchical</td>
	  <td>✔️ - hierarchical</td>
	  <td>✔️ - also extensible with policies</td>
	  </tr>
	  <tr>
	  <td>Remote operations CLI</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  </tr>
	  <tr>
	  <td>Remote operations VCS/GitOps</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  </tr>
	  <tr>
	  <td>SLA</td>
	  <td>99.9% for highers tier</td>
	  <td>N/A</td>
	  <td>❓</td>
	  <td>❓</td>
	  <td>❓</td>
	  </tr>
	  <tr>
	  <td>SSO</td>
	  <td>✅ - only in high paid tiers</td>
	  <td>✅</td>
	  <td>✅ - only in high paid tiers</td>
	  <td>✅ - only in high paid tiers</td>
	  <td>✅</td>
	  </tr>
	  <tr>
	  <td>Secrets Management</td>
	  <td>Internal</td>
	  <td>Vault integrated</td>
	  <td>Internal</td>
	  <td>Internal, AWS, GCP, Azure</td>
	  <td>Internal, also file based</td>
	  </tr>
	  <tr>
	  <td>Short lived environments support</td>
	  <td>❌</td>
	  <td>❌</td>
	  <td>❌</td>
	  <td>✅</td>
	  <td>✅</td>
	  </tr>
	  <tr>
	  <td>State Management</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✔️ - only hidden state</td>
	  <td>✅ - also external</td>
	  </tr>
	  <tr>
	  <td>terraform Provider</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  </tr>
	  <tr>
	  <td>Webhooks</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  <td>✅</td>
	  </tr>
	  </tbody>
	  </table>
- ![](https://uploads-ssl.webflow.com/63e6a81a3b7fbcbcc64af4da/640a03e058678323abbfb0f6_612d11332fb2f666b9db1bed_do-you-need-a-tacos.png){:height 1218, :width 826}
- ![](https://miro.medium.com/v2/resize:fit:2400/1*_hZv2Esx1ba0sPlqwixPEg.png){:height 402, :width 1036}
- {{renderer code_diagram,plantuml}}
	- ```plantuml
	  @startuml
	  mainframe TACOS flow with GitOps
	  
	  actor developer as "Developer"
	  
	  box Git Repository with terraform
	  participant feature as "Feature Branch"
	  participant main as "Main Branch"
	  end box
	  
	  box On-premise/Cloud infrastructure
	  participant flux as "Flux GitOps Agent"
	  participant tacos as "TACOS Git Agent"
	  participant infr_agent as "TACOS Infrastructure Agent"
	  end box
	  
	  
	  box TACOS Provider
	  participant tacos_rest as "TACOS REST API"
	  participant tacos_web  as "TACOS WEB  UI"
	  participant terraform as "Terraform Run"
	  end box
	  
	  box Provisioned Environment
	  participant infra as "Provisioned Infrastructure"
	  end box
	  
	  autonumber
	  developer -> feature: Create a feature branch for\n new Dev environment
	  group  Merge Request
	      feature -> main: merge  request to main branch
	  end
	  
	  group GitOps Reconciliation Loop
	      flux o<->o main: reconciliation loop
	      flux o-> main: detect change
	      flux -> tacos: triggers tacos agent via a webhook
	      main ->o tacos: pulls current status from master
	  end
	  flux -> infr_agent: instruct to create a terraform run
	  
	  group cloud workspace
	      infr_agent -> terraform: Create
	  end
	  terraform -> infra: creates new infrastructure
	  infr_agent -> tacos_rest : trigger run via webhook
	  tacos_web --> developer: run report avaible
	  developer --> infra: access infra, deploy apps
	  @enduml
	  ```