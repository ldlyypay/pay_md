# pay_md
支付信息文档

## IDBI 代收私户
IDBISELFPAYIN

##### 爬取账单规则
``` text
{"Txn Date":"15-01-2025 22:40:00","Value Date":"15/01/2025","Instrument ID":"","CR/DR":"Cr.","Txn Amount":"25000.00","Balance":"25055.71","Description":"UPI/501501259006/PRABHU M"}

"Cr\.".*?"Txn Amount"\s*:\s*"([\d.]+)".*?"Balance"\s*:\s*"([\d.,]+)".*?"Description"\s*:\s*"UPI\/([\d]{12})\/

金额 余额 utr
```

##### 账单导入规则
``` text
{"Txn Date":"15-01-2025 22:40:00","Value Date":"15/01/2025","Instrument ID":"","CR/DR":"Cr.","Txn Amount":"25000.00","Balance":"25055.71","Description":"UPI/501501259006/PRABHU M"}

"Cr\.".*?"Txn Amount"\s*:\s*"([\d.]+)".*?"Balance"\s*:\s*"([\d.,]+)".*?"Description"\s*:\s*"UPI\/([\d]{12})\/

金额 余额 utr
```

## federal one
FEDERALONEPAYIN

##### 爬取账单规则
``` text
{"postingDateString":"28/02/2025 03:10:34 PM","valueDate":"28/02/2025","transRefNo":"S98633619","customerRefNo":"50591510511965      ","credit":48.0,"transactionDetails":"UPI IN/505969513770/9060122275@ptsbi/qwe/5085     ","transactionPostingBranch":"505969513770/qwe              ","sCredit":"48.00","txnAmt":"48.00","txnType":"Credit","runningBalance":"189.00","documentId":"   2","viewProperties":{"highlightRowCSS":"greenGridRow"}}

transactionDetails"\s*:\s*"\s*UPI IN\/([\d]{10,13})\/.*?"sCredit"\s*:\s*"([\d.,]+)".*?"runningBalance"\s*:\s*"([\d.,]+)"

utr 金额 余额
```