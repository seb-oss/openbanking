# Private payment initiation template changes from V8 to V1 condensed version


## Description of changes
Payment initiation (PIS v8) flow was separated to private and corporate, so all private templates was moved to private flow.
Response body schema remains the same for available templates in corporate payments.

---
<br/>

### URLs
| **V8**                                                  | **V1**                                                           |
|---------------------------------------------------------|------------------------------------------------------------------|
| `https://tpp-api.sebgroup.com/tpp/pis/v8/identified2/`  | `https://tpp-api.sebgroup.com/tpp/corporate/pis/v1/identified2/` |
| `https://api-sandbox.sebgroup.com/pis/v8/identified2/`  | `https://api-sandbox.sebgroup.com/corporate/pis/v1/identified2/` |
---
<br/>

## GET /templates
#### comparison of available templates
| **V8**                          | **V1**                                        | **Comments**                   |
|---------------------------------|-----------------------------------------------|--------------------------------|
| `se-domestic-credit-transfers`  | `corporate-se-domestic-credit-transfers`      | Changed template name          |
| _Not present_                   | `corporate-instant-sepa-credit-transfers`     | Changed template name          |
---
<br/>

### HTTP request/response Headers
#### There are no changes in headers between V8 and V1

---
<br/>

## GET /templates/{templateId}
#### changes in responseBody
| **V8**   | **V1**    | **Comments**            |
|----------|-----------|-------------------------|
| `scope`  | _removed_ | scope is defined by url |
---
<br/>

## Templates APIs comparison
<br/>

### GET /templates/corporate-se-domestic-credit-transfers
#### changes in `corporate-se-domestic-credit-transfers` template v1 comparing to `se-domestic-credit-transfers` template v8


| **V8**                                                                           | **V1**                 | **Comments**                       |
|----------------------------------------------------------------------------------|------------------------|------------------------------------|
| _Not present_                                                                    | `creditorAccount.iban` | Removed fields                     |
| `creditorAccount.bban` <br/> `creditorAccount.bgnr` <br/> `creditorAccount.pgnr` | _removed_              | Removed fields                     |
| `creditorAccountMessage`                                                         | _removed_              | Removed fields                     |
---
<br/>

### GET /templates/corporate-instant-sepa-credit-transfers
#### corporate-instant-sepa-credit-transfers is new template and there is no corresponding template in V8

---
<br/>