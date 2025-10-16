
# F to P 

# Test
7018932331 1301002068 9418011750


```sql
select   *
from sec.candidateRegister
where PanchayatCode = 1301002068
```


## Sql Base

## Update clause 

```sql
USE [secExpense]
GO

BEGIN TRANSACTION

-- Update all candidates in this panchayat from F to P
UPDATE sec.candidateRegister
SET ExpStatus = 'P',
    DtTm = GETDATE()
WHERE PanchayatCode = 1301002068
  AND ExpStatus = 'F'

PRINT 'Rows updated: ' + CAST(@@ROWCOUNT AS VARCHAR(10))

-- Verify the change
SELECT AutoID, ExpStatus, DtTm, PanchayatCode
FROM sec.candidateRegister
WHERE PanchayatCode = 1301002068

```

## Editor view ssms for manual del cell val 

```sql
SELECT        ExpenseID, AutoID, expDate, expCode, amtType, amount, paymentDate, voucherBillNumber, payMode, payeeName, payeeAddress, sourceMoney, remarks, DtTm, ExpStatus, amountoutstanding, PanchayatCode
FROM            sec.candidateRegister
WHERE        (PanchayatCode = 1301002068)

```