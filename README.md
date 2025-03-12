# pay_md
支付信息文档

## IDBI 代收私户
IDBISELFPAYIN

##### 账单爬取规则
``` text
{"Txn Date":"15-01-2025 22:40:00","Value Date":"15/01/2025","Instrument ID":"","CR/DR":"Cr.","Txn Amount":"25000.00","Balance":"25055.71","Description":"UPI/501501259006/PRABHU M"}

"Cr\.".*?"Txn Amount"\s*:\s*"([\d.]+)".*?"Balance"\s*:\s*"([\d.,]+)".*?"Description"\s*:\s*"UPI\/([\d]{12})\/

金额 余额 utr
```

##### 账单导入规则
``` text
{"Srl": "1353", "Txn Date": "25/02/202507:20:33", "Value Date": "25/02/2025", "Description": "UPI/542222544784/ZUHABANWER", "Cheque No": "", "CR/DR": "Cr.", "CCY": "INR", "Amount (INR)": "20000.00", "Balance (INR)": "20122.53"}

"Description"\s*:\s*"UPI\/([\d]{12})\/.*?"CR\/DR": "Cr\.".*?"Amount \(INR\)":\s*"([\d.]+)".*?"Balance \(INR\)":\s*"([\d.]+)

utr 金额 余额
```

## federal one
FEDERALONEPAYIN

##### 账单爬取规则
``` text
{"postingDateString":"28/02/2025 03:10:34 PM","valueDate":"28/02/2025","transRefNo":"S98633619","customerRefNo":"50591510511965      ","credit":48.0,"transactionDetails":"UPI IN/505969513770/9060122275@ptsbi/qwe/5085     ","transactionPostingBranch":"505969513770/qwe              ","sCredit":"48.00","txnAmt":"48.00","txnType":"Credit","runningBalance":"189.00","documentId":"   2","viewProperties":{"highlightRowCSS":"greenGridRow"}}

transactionDetails"\s*:\s*"\s*UPI IN\/([\d]{10,13})\/.*?"sCredit"\s*:\s*"([\d.,]+)".*?"runningBalance"\s*:\s*"([\d.,]+)"

utr 金额 余额
```

## canara 不带插件
CANARAPAYIN

##### 账单爬取规则
``` text
{"utr":"436625231975","bill_date":"2024-12-31T18:59:24","transactionType":"C","amount":10,"description":"UPI/CR/436625231975/NADIPUDI /BARB/**44002@pthdfc/NA//PTMdee538e8b4344fd19c5611899323b969/31/12/2024 18:59:24"}

"utr"\s*:\s*"([\d]{10,13})".*?"amount":\s*(\d+).*?,

utr 金额
```

##### 账单导入规则
``` text
{"Txn Date": "09-03-202510:42:00", "Value Date": "09Mar2025", "Cheque No.": "506827753326", "Description": "UPI/CR/506827753326/TANSEERA/JAKA/**15532@ptaxis/zPLX//PTM1f2a478f0ef94593be4645364ab77465/09/03/202510:42:00", "Branch Code": "33", "Debit": "", "Credit": "100.22", "Balance": "6699.59"}

Cheque No."\s*:\s*"([\d]{10,13}).*?"Credit"\s*:\s*"([\d.,]+)".*?"Balance"\s*:\s*"([\d.,]+)"

utr 金额 余额
```