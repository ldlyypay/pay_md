# pay_md
支付信息文档

### IDBI 代收私户

爬取账单规则
``` text
{"Txn Date":"15-01-2025 22:40:00","Value Date":"15/01/2025","Instrument ID":"","CR/DR":"Cr.","Txn Amount":"25000.00","Balance":"25055.71","Description":"UPI/501501259006/PRABHU M"}

"Cr\.".*?"Txn Amount"\s*:\s*"([\d.]+)".*?"Balance"\s*:\s*"([\d.,]+)".*?"Description"\s*:\s*"UPI\/([\d]{12})\/

金额 余额 utr
```

账单导入规则
``` text
{"Txn Date":"15-01-2025 22:40:00","Value Date":"15/01/2025","Instrument ID":"","CR/DR":"Cr.","Txn Amount":"25000.00","Balance":"25055.71","Description":"UPI/501501259006/PRABHU M"}

"Cr\.".*?"Txn Amount"\s*:\s*"([\d.]+)".*?"Balance"\s*:\s*"([\d.,]+)".*?"Description"\s*:\s*"UPI\/([\d]{12})\/

金额 余额 utr
```