- ``` mermaid
  flowchart LR;
  A[Initiation] --> B1[Problem Discovery]
  subgraph Discovery
  B1 --> B2[Resource Discovery]
  B2 --> B3[Solution Discovery]
  end
  
  subgraph B1[Problem Discovery]
    direction TB
    style B1 fill:#aff,stroke:#333,stroke-width:2px
    B11[Problem Statement] --> B12[Pain Points] -->  
    B13[User Journey] --> B14[Constraints] --> B15[Timeline] --> 
    B16(Problem Discovery Document)
    style B16 fill:#2f4
  end
  
  subgraph B2 [Resource Discovery]
    direction TB
    style B2 fill:#aff,stroke:#333,stroke-width:2px
    B21[Scope] --> B22[Resource Availability] --> B23[Fulfillment Team] --> B24(Identified Tech PM)
    style B24 fill:#2f4
  end
  
  subgraph B3 [Solution Discovery]
    direction TB
    style B3 fill:#aff,stroke:#333,stroke-width:2px
    B31[Requirements] -->  B32
    subgraph B32 [Evaluate Proposal]
      direction TB
      B33[Vendor Discussion & Proposal]
      B33 --> B34[Evaluate Proposal]
      B34 --> B35{Meets Requirements?}
      B35 -->|No|B33
      B35 -->|Yes|B36[Budgetary Quote]
    end
    B32 --> B39(Solution Discovery Document)
    style B39 fill:#2f4
  end
  
  B3 --> C1[Preparatory - Tech]
  subgraph Development
  C1 --> C2[System Development]
  B3 --> C3[Preparatory - Business]
  C3 --> C2
  B3 --> C4[Change Mgmt]
  end
  C2 --> D1[Post-Deployment]
  subgraph Post-Deployment
  C3 --> D1
  C4 --> D2[Change Mgmt Continued]
  end
  D1 --> E1[Decommission]
  D2 --> E1
  ```