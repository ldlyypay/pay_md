# 支付信息文档

## 目录索引
- [代收私户](#代收私户)
  - [IDBI 代收私户](#IDBI-代收私户)
  - [BOM 代收私户](#BOM-代收私户)
  - [BOI 代收私户](#BOI-代收私户)
- [代收公户](#代收公户)
  - [BOI 代收公户](#BOI-代收公户)
- [其他银行](#其他银行)
  - [Federal One](#FEDERAl-ONE)
  - [Canara 不带插件](#CANARA-不带插件)


## 代收私户

### <span id="IDBI-代收私户">IDBI 代收私户</span> `IDBISELFPAYIN`

#### 账单爬取规则
##### 示例数据
``` json
{"Txn Date":"15-01-2025 22:40:00","Value Date":"15/01/2025","Instrument ID":"","CR/DR":"Cr.","Txn Amount":"25000.00","Balance":"25055.71","Description":"UPI/501501259006/PRABHU M"}
```
##### 正则表达式
``` javascript
"Cr\.".*?"Txn Amount"\s*:\s*"([\d.]+)".*?"Balance"\s*:\s*"([\d.,]+)".*?"Description"\s*:\s*"UPI\/([\d]{10,13})\/
```
##### 变量名
``` text
金额|余额|utr
```

#### 账单导入规则
##### 示例数据
``` json
{"Srl": "1353", "Txn Date": "25/02/202507:20:33", "Value Date": "25/02/2025", "Description": "UPI/542222544784/ZUHABANWER", "Cheque No": "", "CR/DR": "Cr.", "CCY": "INR", "Amount (INR)": "20000.00", "Balance (INR)": "20122.53"}
```
##### 正则表达式
``` javascript
"Description"\s*:\s*"UPI\/([\d]{10,13})\/.*?"CR\/DR": "Cr\.".*?"Amount \(INR\)":\s*"([\d.]+)".*?"Balance \(INR\)":\s*"([\d.]+)
```
##### 变量名
``` text
utr|金额|余额
```


### <span id="FEDERAl-ONE">federal one</span> `FEDERALONEPAYIN`

#### 账单爬取规则
##### 示例数据
``` json
{"postingDateString":"14/03/2025 02:58:10 PM","valueDate":"14/03/2025","transRefNo":"  S570165","customerRefNo":"50731458844021      ","credit":300.51,"transactionDetails":"UPI IN/226998491575/9649541249@ybl/2oGaB2/5085    ","transactionPostingBranch":"226998491575/2oGaB2           ","sCredit":"300.51","txnAmt":"300.51","txnType":"Credit","runningBalance":"158,682.07","documentId":"   2","viewProperties":{"highlightRowCSS":"greenGridRow"}}
```
##### 正则表达式
``` javascript
transactionPostingBranch"\s*:\s*"([\d]{10,13})\/(2[a-zA-Z\d]{4}2)\s*".*?"sCredit"\s*:\s*"([\d.,]+)".*?"runningBalance"\s*:\s*"([\d.,-]+)"
```
##### 变量名
``` text
utr|随机码|金额|余额
```

#### 账单导入规则
##### 示例数据
``` json
{"Date": "12-03-2025", "Value Date": "12-03-2025", "Particulars": "UPIIN/507183618246/8822344745@pthdfc/2pYPo2/5085", "Tran Type": "TFR", "Tran ID": "S79053642", "Cheque Details": "", "Withdrawals": "", "Deposits": "500.59", "Balance": "3507.49", "Dr/Cr": "CR"}
```
##### 正则表达式
``` javascript
Particulars"\s*:\s*"\s*UPIIN\/([\d]{10,13})\/.*?\/(2[a-zA-Z\d]{4}2)\/.*?"Deposits"\s*:\s*"([\d.,]+)".*?"Balance"\s*:\s*"([\d.,]+)".*?"Dr\/Cr"\s*:\s*"CR"
```
##### 变量名
``` text
utr|随机码|金额|余额
```

### <span id="CANARA-不带插件">canara 不带插件</span> `CANARAPAYIN`

#### 账单爬取规则
##### 示例数据
``` json
{"utr":"974630378636","bill_date":"2025-03-14T15:14:28","transactionType":"C","amount":299.68,"description":"UPI/CR/974630378636/SUNNY SO /PUNB/**36676@ybl/24pKg2//YBL0a8ebb990d994a14abacc719c5ec83b2/14/03/2025 15:14:28"}
```
##### 正则表达式
``` javascript
"utr"\s*:\s*"([\d]{10,13})".*?"amount":\s*([\d.,]+),.*?"description"\s*:\s*".*?\/(2[a-zA-Z\d]{4}2)\/
```
##### 变量名
``` text
utr|金额
```

#### 账单导入规则
##### 示例数据
``` json
{"Txn Date": "09-03-202510:42:00", "Value Date": "09Mar2025", "Cheque No.": "506827753326", "Description": "UPI/CR/506827753326/TANSEERA/JAKA/**15532@ptaxis/zPLX//PTM1f2a478f0ef94593be4645364ab77465/09/03/202510:42:00", "Branch Code": "33", "Debit": "", "Credit": "100.22", "Balance": "6699.59"}
```
##### 正则表达式
``` javascript
Cheque No."\s*:\s*"([\d]{10,13}).*?"Credit"\s*:\s*"([\d.,]+)".*?"Balance"\s*:\s*"([\d.,]+)"
```
##### 变量名
``` text
utr|金额|余额
```

### <span id="BOM-代收私户">BOM 代收私户</span> `BOMSELFPAYIN`

#### 账单爬取规则(账单导入共用)
##### 示例数据
``` json
{"Date":"22/12/2024","Particulars":"UPI 577543261714/AIRP/Jatothu Akhil/Payment from P","Cheque/Reference No":"","Debit":"","Credit":"100.00 INR","Balance":"25100.00 INR","Channel":"Internet Banking"}
```
##### 正则表达式
``` javascript
"Particulars"\s*:\s*"UPI\s*(\d{10,13})\/.*?"\s*,\s*"Credit"\s*:\s*"([\d.,]+)\s*.*?"\s*,\s*"Balance"\s*:\s*"([\d.,]+)\s*.*?"
```
##### 变量名
``` text
utr|金额|余额
```

### <span id="BOI-代收公户">BOI 代收公户</span> `BOIPAYIN`

#### 账单爬取规则
##### 示例数据
``` json
{"date":"Friday,November8,20242:48PM","description":"UPI/983647117743/CR/MrRAJ/IDIB/rajan2312/Paymen","cheque_no":"","currency":"INR","debit":"","credit":"5000.00","balance":"5000.00"}
```
##### 正则表达式
``` javascript
"description"\s*:\s*".*?([\d]{10,13}).*?".*?"credit"\s*:\s*"([\d.,]+)".*?"balance"\s*:\s*"([\d.,]+)"
```
##### 变量名
``` text
utr|金额|余额
```

### <span id="BOI-代收私户">BOI 代收私户</span> `BOISELFPAYIN`

#### 账单爬取规则
##### 示例数据
``` json
{"date":"Wednesday,September25,20243:33PM","description":"UPI/426913102501/CR/RUPEND/ICIC/844709453/Paidv","cheque_no":"","currency":"INR","debit":"","credit":"10001.00","balance":"10001.00"}
```
##### 正则表达式
``` javascript
"description"\s*:\s*".*?([\d]{10,13}).*?".*?"credit"\s*:\s*"([\d.,]+)".*?"balance"\s*:\s*"([\d.,]+)"
```
##### 变量名
``` text
utr|金额|余额
```