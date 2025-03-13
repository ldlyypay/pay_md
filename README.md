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
{"postingDateString":"28/02/2025 03:10:34 PM","valueDate":"28/02/2025","transRefNo":"S98633619","customerRefNo":"50591510511965      ","credit":48.0,"transactionDetails":"UPI IN/505969513770/9060122275@ptsbi/qwe/5085     ","transactionPostingBranch":"505969513770/qwe              ","sCredit":"48.00","txnAmt":"48.00","txnType":"Credit","runningBalance":"189.00","documentId":"   2","viewProperties":{"highlightRowCSS":"greenGridRow"}}
```
##### 正则表达式
``` javascript
transactionDetails"\s*:\s*"\s*UPI IN\/([\d]{10,13})\/.*?"sCredit"\s*:\s*"([\d.,]+)".*?"runningBalance"\s*:\s*"([\d.,-]+)"
```
##### 变量名
``` text
utr|金额|余额
```

#### 账单导入规则
##### 示例数据
``` json
{"Date": "12-03-2025", "Value Date": "12-03-2025", "Particulars": "UPIIN/507183618246/8822344745@pthdfc/pYPo/5085", "Tran Type": "TFR", "Tran ID": "S79053642", "Cheque Details": "", "Withdrawals": "", "Deposits": "500.59", "Balance": "3507.49", "Dr/Cr": "CR"}
```
##### 正则表达式
``` javascript
Particulars"\s*:\s*"\s*UPIIN\/([\d]{10,13})\/.*?"Deposits"\s*:\s*"([\d.,]+)".*?"Balance"\s*:\s*"([\d.,]+)".*?"Dr\/Cr"\s*:\s*"CR"
```
##### 变量名
``` text
utr|金额|余额
```

### <span id="CANARA-不带插件">canara 不带插件</span> `CANARAPAYIN`

#### 账单爬取规则
##### 示例数据
``` json
{"utr":"436625231975","bill_date":"2024-12-31T18:59:24","transactionType":"C","amount":10,"description":"UPI/CR/436625231975/NADIPUDI /BARB/**44002@pthdfc/NA//PTMdee538e8b4344fd19c5611899323b969/31/12/2024 18:59:24"}
```
##### 正则表达式
``` javascript
"utr"\s*:\s*"([\d]{10,13})".*?"amount":\s*(\d+).*?,
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