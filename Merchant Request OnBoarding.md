1. Setup Jira Task
   1. 448 Epic
   2. Set Inprogress
   3. Assign to myself
   4. Check approved
2. file:
   1. https://docs.google.com/spreadsheets/d/10KPVWvcJzxCcy3PZd3CB2HIodfyIyJ83aIFcer7EuV4/edit#gid=1327463790
   2. https://docs.google.com/spreadsheets/d/1bAuiwtbDfnbuh_7CdGIkwyvHIABu1YnqvLMosnGmhpc/edit#gid=1894051458
   3. https://docs.google.com/spreadsheets/d/1GnKQQUnjD4NrVrsgyjamKYibJmYNAgbIjYQ1vYuc06Q/edit#gid=1070173015
3. Masukin data kedalam `upsert_merchant` dan `upsert_owner`
4. Perbaiki data di sheet `upsert_merchant` dan `upsert_owner` jika ada koma (,), maka harus gunakan petik dua ("")
5. Perbaiki data kabupaten/kota alamat sesuai dengan enumeration dan nomor telp `upsert_merchant`
6. cek seluruh NPWP (15 digit saja)
7. 
   ```
      gsts
      aws --profile DeddyChandra@tvlk-mfc-prod ssm start-session --target i-0259605d566873963
      bash
      cd ~
      cd mf-plutus-scripts/merchant-lending-scripts/merchants/
   ```
8. copy data dari sheet `upsert_merchant`, masukin ke dalam `upsert_merchant.csv` menggunakan vim
9. run command `:%s/\t/,/g` untuk melakukan regex
10. ```
      pipenv run python upsert_merchant.py --env prod upsert_merchant.csv
   ```
11. cat `upsert_merchant.csv.log` buat cek
12. copy data dari sheet `upsert_owner`, masukin ke dalam `upsert_owner.csv` menggunakan vim
13. run command `:%s/\t/,/g` untuk melakukan regex
14. ```
      pipenv run python upsert_owner.py --env prod upsert_owner.csv
   ```
14. cat `upsert_owner.csv.log` buat cek
15. report ke Vindy