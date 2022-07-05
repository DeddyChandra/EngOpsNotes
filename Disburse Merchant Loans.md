# Disburse Merchant Loans
1. Setup Jira Task
   1. 448 Epic
   2. Set Inprogress
   3. Assign to myself
   4. Check approved
2. file:
   1. https://docs.google.com/spreadsheets/d/10KPVWvcJzxCcy3PZd3CB2HIodfyIyJ83aIFcer7EuV4/edit#gid=1327463790
   2. https://docs.google.com/spreadsheets/d/1bAuiwtbDfnbuh_7CdGIkwyvHIABu1YnqvLMosnGmhpc/edit#gid=1894051458
   3. https://docs.google.com/spreadsheets/d/1GnKQQUnjD4NrVrsgyjamKYibJmYNAgbIjYQ1vYuc06Q/edit#gid=1070173015
<!-- 3. ```
      prod-db: aws --profile mfc-prod ssm start-session --target i-0c32e4013fae2d309
      prod-bastion: aws --profile mfc-prod ssm start-session --target i-0259605d566873963
   ```
4. DB password
   ```
      User_ ro_user
      7Lg3H$eY9#KBeFKQVRTh
   ```
5. connect DB
   ```
      psql -h mfcmlms-postgres-0e3a534c1dea98d8.cmzemiutf0bp.ap-southeast-1.rds.amazonaws.com -U ro_user -p 5432 -d merchantlending
   ``` -->
3. Buat cari loanId 
   ```
      curl https://mfcmlms.prod.mfc.tvlk-pay.cloud/v1/loans?loanExternalId=<loanId> | python3 -m json.tool
   ```
4. masukin data ke sheet `update_loan_status`, loanStatus diganti jadi `LOAN_AGREEMENT_SIGNED`
5. Start aws production
   ```
      gsts
      aws --profile DeddyChandra@tvlk-mfc-prod ssm start-session --target i-0259605d566873963
      bash
      cd mf-plutus-scripts/merchant-lending-scripts/loans/
   ```
6. copy data dari sheet `update_loan_status`, masukin ke dalam `update_loan_status.csv` menggunakan vim
7. run command di dalam vim untuk melakukan regex
   ```
      `:%s/\t/,/g`
   ```
8. execute `update_loan_status.py`
   ```
      pipenv run python update_loan_status.py --env prod update_loan_status.csv
   ```
9. buat cek
   ```
      cat update_loan_status.csv.log
   ```
10. sheet `update_loan_status`, loanStatus diganti jadi `OUTSTANDING`
11. copy data dari sheet `update_loan_status`, masukin ke dalam `update_loan_status.csv` menggunakan vim
12. run command di dalam vim untuk melakukan regex
   ```
      `:%s/\t/,/g`
   ```
13. execute `update_loan_status.py` 
   ```
      pipenv run python update_loan_status.py --env prod update_loan_status.csv
   ```
14. buat cek
   ```
      cat update_loan_status.csv.log
   ```
