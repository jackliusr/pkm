- Total Return Swap (TRS): a swap agreement in which one party makes payments based on a set rate, either fixed or variable, while the other party makes payments based on the return of an underlying asset, which includes both the income it generates and any capital gains. In total return swaps, the underlying asset, referred to as the reference asset, is usually an equity index, a basket of loans, or bonds. The asset is owned by the party receiving the set rate payment.
- **Core banking** is a back-end system that connects multiple branches of the same bank together to deliver operations like loan management, withdrawals, deposits and payments in real-time.
- CORE stands for Centralized Online Real-time Environment
- core banking features
- Insurance Application Architecture (IAA)
	- Entities:
	  collapsed:: true
		- **Policyholder:**
			- Attributes: PolicyholderID (Primary Key), FirstName, LastName, DateOfBirth, ContactInfo, SSN, etc.
		- **Insurance Policy:**
			- Attributes: PolicyID (Primary Key), PolicyNumber, PolicyType, PolicyStartDate, PolicyEndDate, PremiumAmount, CoverageAmount, etc.
		- **Coverage Type:**
			- Attributes: CoverageTypeID (Primary Key), CoverageName, Description, PremiumRate, etc.
		- **Claim:**
			- Attributes: ClaimID (Primary Key), PolicyID (Foreign Key), ClaimDate, ClaimStatus, ClaimAmount, Description, etc.
		- **Beneficiary:**
			- Attributes: BeneficiaryID (Primary Key), FirstName, LastName, DateOfBirth, Relationship, ContactInfo, etc.
		- **Insurance Agent:**
			- Attributes: AgentID (Primary Key), FirstName, LastName, ContactInfo, HireDate, etc.
		- **Insurance Company:**
			- Attributes: CompanyID (Primary Key), CompanyName, Address, ContactInfo, RegistrationDate, etc.
		- **Payment Transaction:**
			- Attributes: TransactionID (Primary Key), PolicyID (Foreign Key), TransactionDate, Amount, PaymentMethod, TransactionStatus, etc.
	- relationships: 
	  ``` mermaid
	  erDiagram
	    Policyholder ||..|{ Policy : has
	    Policy }|..|| CoverType : associate
	    Policyholder ||..|{Claim: make
	    Claim }|..||Policy: associate
	    Policy }|..|{Beneficiary: associate
	    InsuranceAgent ||..|{Policy: assign
	    InsuranceCompany ||..|{Police: provide
	    PaymentTransactions ||..|{Policy: relate
	  ```