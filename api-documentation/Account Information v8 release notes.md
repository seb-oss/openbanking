
# Account Information Services changes from V7 to V8 condensed version

## /accounts

### OAS

| **V7** | **V8** | **Comments** |
| --- | --- | --- |
| `bicAddress`<br/> | _removed_  |  |
|`accountInterest`<br/> | _removed_  |  |
|`cardLinkedToAccountbankgiroNumber`<br/> | _removed_  |  |
|`accountOwners`<br/> | _removed_  |  |
|`aliasespaymentService` | _removed_  |  |

### Private
> __For private accounts the ResourceId will be different in V8 compared to V7__

| **V7** | **V8** | **Comments** |
| --- | --- | --- |
| | `bic`|  |
| Amounts in x decimals| Amounts in 3 decimals  |
| _closed accounts_ currency with value "xxx" | removed _closed accounts_ currency | There will be no currency when listing closed accounts. |

### Corporate

| **V7** | **V8** | **Comments** |
| --- | --- | --- |
| `OwnerName` sometimes null | `OwnerName` always set |   |
| `cardLinkedTAccount`, `aliases` and `paymentService` always present  | `cardLinkedTAccount`, `aliases` and `paymentService` present only through `account/{accountId}` | These two fields were previously present when listing accounts for corporate customers. To make the API consistent for private and cooperate customers this information is now only available when retrieving a single account.  |

## /accounts/{accountId}

### Private
> __For private accounts the ResourceId will be different in V8 compared to V7__

| **V7** | **V8** | **Comments** |
| --- | --- | --- |
| `bankgironumber` | moved into `aliases` | |
| Amounts in x decimals | Amounts in 3 decimals  |
| Field has the name `accountOwners`:<br/><br/>_(Olle logged in)_<br/>ownerName: __Olle__<br/>accountOwners: __[Karin]__<br/><br/>(_Karin logged in_)<br/>ownerName: __Karin__<br/>accountOwners: __[Karin]__ | Field has the name `additionalOwnerNames`:<br/><br/>_(Olle logged in)_<br/>ownerName: __Olle__<br/>`additionalOwnerNames`: __[Karin]__<br/><br/>(_Karin logged in_)<br/>`ownerName`: __Karin__<br/>`additionalOwnerNames`: __[Olle]__| The field accountOwners has been changed to `additionalOwnerNames` and the list will now contain the names that are owners of the accounts that are not the logged in user.|
| _closed accounts_ currency with value "xxx" | removed _closed accounts_ currency | There will be no currency when listing closed accounts. |

| `accountInterest` with one decimal.  | `accountInterest` with six decimals.  ||
| `CreditLine` present with value 0.00 | `CreditLine` only present when flag withBalance=true | Creditline will now only be present when you set the `withBalance` flag to true.  |

### Corporate

| **V7** | **V8** | **Comments** |
| --- | --- | --- |
| `interestType`: _inherited from ledger_ | `interestType`: <code>Credit&#124;Debit&#124;Penalty&#124;CreditAdjust&#124;DebitAdjust&#124;PenaltyAdjust</code> | |
| `interestRateType`: <code>"Fixed&#124;FIXED"</code> | `interestRateType: "Fixed"` | |
| `interestRateType: "ORD"` | `interestRateType: "Regular"` | |
| `interestRateType: "Base"` | `interestRateType: "BaseRate"` | |
| `calculationBase: "per band"` | `calculationBase: "perTier"` | |
| <code>EXT&#124;INT</code> | <code>External&#124;Internal</code> | |
| `OwnerName` sometimes null | `OwnerName` always set |   |
| Field values for `interestConditions`, `interests.posted` and `interests.accrued` are not harmonized e.g. field can have value `y/n` and `true/false` depending on ledger.<br/><br/>Example for account type 1:<br/>`"pdAccountability": "External"`,<br/>`"accruedCreditInterestIndicator": "true"`,<br/>`"accruedDebitInterestIndicator": "false"`<br/><br/>Example for account type 2:<br/>`"pdAccountability": "EXT"`,<br/>`"accruedCreditInterestIndicator": "Y"`,<br/>`"accruedDebitInterestIndicator": "N"` | Field values for `interestConditions`, `interests.posted` and `interests.accrued` are harmonized e.g. field will have now only have the value `true/false`.<br/><br/>Example for account type 1:<br/>`"pdAccountability": "External"`, <br/>`"accruedCreditInterestIndicator": "true"`,<br/>`"accruedDebitInterestIndicator": "false"`<br/><br/>Example for account type 2:<br/>`"pdAccountability": "External"`,<br/>`"accruedCreditInterestIndicator": "true"`,<br/>`"accruedDebitInterestIndicator": "false"`| Interest information should now be consistent regardless of which account type is used and supplied in the same format.  |
| Rates has no formatting | Rates will be formatted to 6 decimals |
 |
 
## /accounts/{accountId}/balances

| **V7** | **V8** | **Comments** |
| --- | --- | --- |
| Balance with 2-3 decimals | Balance with 3 decimals |
 |

## /accounts/{accountId}/transactions

| **V7** | **V8** | **Comments** |
| --- | --- | --- |
| – | `bic` present in V8 private | You will now get the `bic` of the account when listing accounts for private customers. |
| `proprietaryBankTransactionCodeText` set by `"Stående överföring"` | `proprietaryBankTransactionCodeText` will have values stated in english for both corporate and private customers e.g. `"Standing transfer"` | The text will now always be in English.  |
| `proprietaryBankTransactionCode` | _removed_ | |
| Maximum 199 booked transaction in one response.  | Max 500 booked transaction in one response.  | |
| `transactionId: x` | `transactionId: y` | For private customers the `transactionId` will be different in v7 and v8 for the same transaction.  |
| `remittanceInformationUnstructured` or `remittanceInformationUnstructuredArray` is used.<br/><br/>`remittanceInformationUnstructured` : <br/>`"text"`<br/>`remittanceInformationUnstructuredArray` : `["text","text2"]` | Only `remittanceInformationUnstructuredArray` is used.<br/><br/>`remittanceInformationUnstructuredArray`  : `["text"]`<br/><br/>`remittanceInformationUnstructuredArray`  : `["text","text2"]` | `remittanceInformationUnstructured` Is no longer present in the v7 API. In v8 remittanceInformationUnstructuredArray will always be used instead. |
| Upcoming events field `creditorName` is present<br/>`"creditorName": "987fd64d-Ab9"`, | Upcoming events field `creditorName` is replaced by `CreditorAccount` and `descriptiveText`:<br/><br/>`"creditorAccount": "816619843227316"`,<br/>`"descriptiveText": "987FD64D-AB9"` | |
| For `futureEvents` pending amount is always positive  | For `futureEvents` pending amount can now be negative | The amounts in pending events can now be negative for private users. Was always positive previously.  |
| Link to the next page will have the format: `/accounts/df0f49fb-3417-4076-a514-77e23f8e0acc/transactions?bookingStatus=booked&dateFrom=2021-04-20&transactionSequenceNumber=1"` | Link to the next page will have the format:`/accounts/204f1c7b-959c-451e-b29a-dba44695e8e7/transactions?bookingStatus=booked&paginationKey=P9OvCmOTdnKsD3X5qiQYU885EVQBgdAItSgqKkqMnSS1..KCoqSoydJB4bKkc12T\_duHK9MPbvTT3fpZSvFRurqLUoKipKjJ0kVH4F0qRsss8\_y15rPumEdybJ5sBU4Fam` | |
| `transactionSequenceNumber` is the parameter name for _paging_ | `paginationKey` is the parameter name for _paging_ |  |

## /accounts/{accountId}/transactions/{transactionId}

| **V7** | **V8** | **Comments** |
| --- | --- | --- |
| — | `proprietaryBankTransactionCodeText` will have specific values e.g. "Standing transfer" | |

### BG\_PG

| **V7** | **V8** | **Comments** |
| --- | --- | --- |
| `"creditorAccount"`: <br/>`{"bban": "9019506"}`| `"creditorAccount"`: <br/>`{"plusgiroNumber": "9019506"}` | V8 will now correctly show transactions to plusgironumber. |

### Swish

| **V7** | **V8** | **Comments** |
| --- | --- | --- |
| | `"transactionTime":"2020-04-07T08:44:13"`,<br/>`"creditorNameAndAddress": "TACTEL, REGRESSIONSTESTKUND"`,<br/>`"debtorName":"OMARI PITMAN"`,<br/>`"orderId": "6336195730728041"` | You will in V8 receive the `transactionTime` and the _name_ of the sender/receiver for Swish transactions for private customers. |

### Card

<table><thead><tr><td>V7</td><td>V8</td><td>Comments</td></tr></thead>
<tr><td>
<pre><code>{
    "transactionAmount": {
        "amount": "-253.000",
        "currency": "SEK"
    },
    "proprietaryBankTransactionCode": "051",
    "valueDate": "2021-08-17",
    "bookingDate": "2021-08-17",
    "debtorAccount": {
        "bban": "52801062510",
        "bic": "ESSESESSXXX"
    },
    "remittanceInformationUnstructured": "HAMBURG",
    "currencyExchange": {
        "exchangeRate": "10,1200"
    },
    "transactionDate": "2021-08-17",
    "originalAmount": {
        "amount": "-25.000",
        "currency": "EUR"
    }
}</code></pre>
</td><td><pre><code>{  
    "bookingDate": "2021-08-17",  
    "cardAcceptorId": "LIDL",  
    "currencyExchange": {  
        "exchangeRate": "10.120000"  
    },  
    "debtorAccount": {  
        "bban": "52801062510",  
        "bic": "ESSESESSXXX"  
    },  
    "originalAmount": {  
        "amount": "-25.000",  
        "currency": "EUR"  
    },  
    "proprietaryBankTransactionCodeText": "Card foreign purchase",  
    "remittanceInformationUnstructuredArray": [  
        "HAMBURG"  
    ],  
    "transactionAmount": {  
        "amount": "-253.000",  
        "currency": "SEK"  
    },  
    "transactionDate": "2021-08-16",  
    "valueDate": "2021-08-17"  
}</code></pre></td><td><code>CardAcceptorId</code> is now present. <code>remittanceInformationUnstructured</code> has been removed and <code>remittanceInformationUnstructuredArray</code> is used instead.
No trailing blankspace in the field <code>remittanceInformationUnstructured</code>.
<code>transactionDate</code> is set to the correct date.
<code>exchangeRate</code> with 6 decimals</td>
</table>