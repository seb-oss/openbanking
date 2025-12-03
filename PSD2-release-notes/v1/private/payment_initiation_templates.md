# Private payment initiation template changes from V8 to V1 condensed version


## Description of changes
Payment initiation (PIS v8) flow was separated to private and corporate, so all corporate templates was moved to [corporate flow](https://google.com).
Response body schema remains the same for available templates in private payments.

---
<br/>

### URLs
| **V8**                                                  | **V1**                                                         |
|---------------------------------------------------------|----------------------------------------------------------------|
| `https://tpp-api.sebgroup.com/tpp/pis/v8/identified2/`  | `https://tpp-api.sebgroup.com/tpp/private/pis/v1/identified2/` |
| `https://api-sandbox.sebgroup.com/pis/v8/identified2/`  | `NOT CLEAR YET`                                                |
---
<br/>

## GET /templates
#### comparison of available templates
| **V8**                                             | **V1**                                       | **Comments**                   |
|----------------------------------------------------|----------------------------------------------|--------------------------------|
| `swedish-domestic-private-credit-transfers`        | `private-se-domestic-credit-transfers`       | Changed template name          |
| `swedish-domestic-private-own-accounts-transfers`  | `private-se-domestic-own-credit-transfers`   | Changed template name          |
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

### GET /templates/private-se-domestic-credit-transfers 
#### changes in `private-se-domestic-credit-transfers` template v1 comparing to `swedish-domestic-private-credit-transfers` template v8


| **V8**                           | **V1**                                                                                           | **Comments**                      |
|----------------------------------|--------------------------------------------------------------------------------------------------|-----------------------------------|
| `templateId`                     | `templateId`                                                                                     | Changed from required to optional | 
| _Not present_                    | `debtorAccount.bban`                                                                             | Added new field                   |
| _Not present_                    | `creditorName`                                                                                   | Added new mandatory field         |
| _Not present_                    | `remittanceInformationUnstructured`                                                              | Added new field                   |
| _Not present_                    | `remittanceInformationStructured.reference`<br/> `remittanceInformationStructured.referenceType` | Added new fields                  |
| `creditorAccount.bban`           | _removed_                                                                                        | Removed fields                    |
| `creditorAccountMessage`         | _removed_                                                                                        | Removed fields                    |
---
<br/>

### GET /templates/swedish-domestic-private-own-accounts-transfers
#### changes in `private-se-domestic-own-credit-transfers` template v1 comparing to `swedish-domestic-private-own-accounts-transfers` template v8
| **V8**                            | **V1**                              | **Comments**                      |
|-----------------------------------|-------------------------------------|-----------------------------------|
| `templateId`<br/>                 | `templateId`                        | Changed from required to optional |
| _Not present_<br/>                | `debtorAccount.bban`                | Added new field                   |
| _Not present_<br/>                | `remittanceInformationUnstructured` | Added new field                   |
| `creditorAccountMessage`<br/>     | _removed_                           | Removed fields                    |
---
<br/>