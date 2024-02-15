- 5 Key components
	- Customer Management
	  collapsed:: true
		- Customer Information
		- KYC (Know Your Customer)
		- Customer Onboarding
		- Customer Segmentation
		- Customer Relationship Management (CRM)
	- Account Management
	  collapsed:: true
		- Account Opening
		- Account Types (Savings, Current, Fixed Deposit, etc.)
		- Account Balance Management
		- Account Statements
		- Interest Calculation
		- Account Closure
		- Overdraft Facilities
	- Transaction Processing
	  collapsed:: true
		- Deposits
		- Withdrawals
		- Fund Transfers
		- Cheque Processing
		- Clearing and Settlement
		- Standing Instructions
		- Automatic Payments
	- Loan Management
	  collapsed:: true
		- Loan Application Processing
		- Loan Approval
		- Loan Disbursement
		- Loan Repayment Tracking
		- Interest Calculation
		- Collateral Management
		- Loan Account Statements
	- Risk Management
	  collapsed:: true
		- Credit Risk Assessment
		- Risk Scoring
		- Anti-Money Laundering (AML)
		- Fraud Detection and Prevention
		- Compliance Monitoring
		- Reporting and Analytics
- Core ERD
  ``` mermaid
  erDiagram
      Customer ||..|{ Account : has
      Account ||..|{ Transaction: has
      Branch ||..|{ Account: Maintain
      Loan   }|..||Account: Borrow
  ```
- Risk
  ``` mermaid
  erDiagram
      Risk ||..|{ RiskCategory : has
      RiskOwner ||..|{ Risk: Own
      RiskMitigation ||..|| Risk: Mitigate 
      RiskCategory {
          number CategoryID
          string Name
      }
      Risk {
          number RiskID
          string Description
          number Likelihood
          string Impact
      }
      RiskOwner{
          number OwnerID
          string Role
          string Name
      }
      RiskMitigation{
          number MitigationID
          string Description
          date PlannedStartDate
          date PlannedEndDate
      }
  ```
- Bank anatomy based on a next generation core banking platform
  ![Bank anatomy](https://www.mckinsey.com/~/media/mckinsey/industries/financial%20services/banking%20blog/next%20generation%20core%20banking%20platforms%20a%20golden%20ticket/corebanking_804_ex1_v3.png?cq=50&cpy=Center){:height 440, :width 609}
-