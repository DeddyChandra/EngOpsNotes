# Approve Merchant Application and Send Loan Draft Agreement
1. Setup Jira Task
   1. 448 Epic
   2. Set Inprogress
   3. Assign to myself
   4. Check approved
2. file:
   1. https://docs.google.com/spreadsheets/d/10KPVWvcJzxCcy3PZd3CB2HIodfyIyJ83aIFcer7EuV4/edit#gid=1327463790
   2. https://docs.google.com/spreadsheets/d/1bAuiwtbDfnbuh_7CdGIkwyvHIABu1YnqvLMosnGmhpc/edit#gid=1894051458
   3. https://docs.google.com/spreadsheets/d/1GnKQQUnjD4NrVrsgyjamKYibJmYNAgbIjYQ1vYuc06Q/edit#gid=1070173015
3. ada 3 step
   1. Update merchant application kalao status masih waiting decision
   2. Insert_loan trus masukin id
   3. Pending loan agreement
4. lihat sheet `update_merchant_application` kalao status masih waiting decision harus diupdate jadi approve
5. sheet `update_merchant_application` `decision` ganti jadi `APPROVED`
   ```
      curl https://mfcmlms.prod.mfc.tvlk-pay.cloud/v1/merchants/GETSTOK-<email>/applications | python3 -m json.tool
   ```
6. masukin data di sheet `update_merchant_application`
7. start connect ke aws prod
   ```
      gsts
      aws --profile DeddyChandra@tvlk-mfc-prod ssm start-session --target i-0259605d566873963
      bash
      cd mf-plutus-scripts/merchant-lending-scripts/merchants/
   ```
8. copy data dari sheet `update_merchant_application`, masukin ke dalam `update_merchant_application.csv` menggunakan vim
9. run command di dalam vim untuk melakukan regex
   ```
      :%s/\t/,/g
   ```
10. command untuk execute `update_merchant_application.py`
   ```
      pipenv run python update_merchant_application.py --env prod update_merchant_application.csv
   ```
11. cat `update_merchant_application.csv.log` buat cek
12. buat cek
   ```
      curl https://mfcmlms.prod.mfc.tvlk-pay.cloud/v1/merchants/GETSTOK-<email>.com/applications | python3 -m json.tool
   ```
13. pindah direktori ke loans
   ```
      cd ../loans/
   ```
14. masukin data di sheet `insert_loan`
15. copy data dari sheet `insert_loan`, masukin ke dalam `insert_loan.csv` menggunakan vim
16. run command di dalam vim untuk melakukan regex
   ```
      :%s/\t/,/g
   ```
17. execute `insert_loan.py`
   ```
      pipenv run python insert_loan.py --env prod insert_loan.csv
   ```
18. buat cek
   ```
      cat insert_loan.csv.log
   ```
20. masukin data di sheet `update_loan_status`, set loanStatus menjadi `PENDING_LOAN_AGREEMENT`
21. copy data dari sheet `update_loan_status`, masukin ke dalam `update_loan_status.csv` menggunakan vim
22. run command di dalam vim untuk melakukan regex
   ```
      :%s/\t/,/g
   ```
23. execute `update_loan_status.py`
   ```
      pipenv run python update_loan_status.py --env prod update_loan_status.csv
   ```
23. buat cek
   ```
      cat update_loan_status.csv.log
   ```
