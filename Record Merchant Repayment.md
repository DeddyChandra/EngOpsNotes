# Merchant Repayment
1. Setup Jira Task
   1. 448 Epic
   2. Set Inprogress
   3. Assign to myself
   4. Check approved
2. file:
   1. https://docs.google.com/spreadsheets/d/10KPVWvcJzxCcy3PZd3CB2HIodfyIyJ83aIFcer7EuV4/edit#gid=1327463790
   2. https://docs.google.com/spreadsheets/d/1bAuiwtbDfnbuh_7CdGIkwyvHIABu1YnqvLMosnGmhpc/edit#gid=1894051458
   3. https://docs.google.com/spreadsheets/d/1GnKQQUnjD4NrVrsgyjamKYibJmYNAgbIjYQ1vYuc06Q/edit#gid=1070173015
3. masukin data ke dalam sheet `repayment`
4. start aws production
   ```
      gsts
      aws --profile DeddyChandra@tvlk-mfc-prod ssm start-session --target i-0259605d566873963
      bash
      curl https://mfcmlms.prod.mfc.tvlk-pay.cloud/v1/loans?loanExternalId=<loanId> | python3 -m json.tool
   ```
5. Ambil `loanId` dari hasil curl dan masukin kedalam sheet `repayment`
6. Ganti tanggal `PaidOn`
7. pindah directory ke repayments
   ```
      cd mf-plutus-scripts/merchant-lending-scripts/repayments/
   ```
8. copy data dari sheet `insert_repayment.csv`, masukin ke dalam `insert_repayment.csv` menggunakan vim
9. run command di dalam vim untuk melakukan regex
   ```
      :%s/\t/,/g
   ```
10. execute `insert_repayment.py`
   ```
      pipenv run python insert_repayment.py --env prod insert_repayment.csv
   ```
11. buat cek
   ```
      cat insert_repayment.csv.log
   ```
12. report ke Vindy
