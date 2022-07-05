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
6. Buat cari loanId 
   ```
      curl https://mfcmlms.prod.mfc.tvlk-pay.cloud/v1/loans?loanExternalId=<loanId> | python3 -m json.tool
   ```
7. masukin data ke sheet `update_loan_status`, loanStatus diganti jadi `LOAN_AGREEMENT_SIGNED`
8. ```
      gsts
      aws --profile DeddyChandra@tvlk-mfc-prod ssm start-session --target i-0259605d566873963
      bash
      cd mf-plutus-scripts/merchant-lending-scripts/loans/
   ```
9.  copy data dari sheet `update_loan_status`, masukin ke dalam `update_loan_status.csv` menggunakan vim
10. run command `:%s/\t/,/g` untuk melakukan regex
11. ```
      pipenv run python update_loan_status.py --env prod update_loan_status.csv
   ```
12. `cat update_loan_status.csv.log` buat cek
13. sheet `update_loan_status`, loanStatus diganti jadi `OUTSTANDING`
14. copy data dari sheet `update_loan_status`, masukin ke dalam `update_loan_status.csv` menggunakan vim
15. run command `:%s/\t/,/g` untuk melakukan regex
16. ```
      pipenv run python update_loan_status.py --env prod update_loan_status.csv
   ```
17. `cat update_loan_status.csv.log` buat cek