- When UAT has passed, send for **first scan** by VAPT vendor - black and grey testing.
- Report for findings (Low, Medium, High) will be prepared by the VAPT vendor. TA and app vendor can review the report to understand the findings discovered.
- App vendor to remediate the findings (e.g. to bring down all risks to at least Low).
- VAPT vendor to **rescan** for findings identified by Step 1.
- Report will be prepared by the VAPT vendor. TA to review the report to make sure all findings have been remediated accordingly.
- PM forward report to Andy, it will be reviewed by Security (Andy) for green light to go-live.
- medium and high risk items
  ```mermaid
  flowchart
      risk(medium and high risk items)-->registry(register to Peter)
      registry-->accept(accept risk report)
  ```
- risk acceptance form
- https://sntuc.sharepoint.com/sites/itd/ItdOnly/ITSO%20Monthly%20Meeting/Forms/AllItems.aspx?id=%2Fsites%2Fitd%2FItdOnly%2FITSO%20Monthly%20Meeting%2FIT%20Governance%2FIT%20Policies%2FIT%2DPO%2D23%20Vulnerability%20Assessment%20and%20Penetration%20Testing%20and%20Source%20Code%20Policy%2Epdf&viewid=38eca265%2Dc381%2D4704%2D8879%2D2b01163d0998&parent=%2Fsites%2Fitd%2FItdOnly%2FITSO%20Monthly%20Meeting%2FIT%20Governance%2FIT%20Policies