# Private periodic payment initiation changes from V8 to V1 condensed version

## Description of changes
#### Payment initiation (PIS v8) flow was separated to private and corporate, <br/> this changes is acceptable for private flow only.

---
<br/>

### URLs
| **V8**                                                  | **V1**                                                          |
|---------------------------------------------------------|-----------------------------------------------------------------|
| `https://tpp-api.sebgroup.com/tpp/pis/v8/identified2/`  | `https://tpp-api.sebgroup.com/tpp/private/pis/v1/identified2/`  |
| `https://api-sandbox.sebgroup.com/pis/v8/identified2/`  | `https://api-sandbox.sebgroup.com/private/pis/v1/identified2/`  |
---
<br/>

### PATHs
| **V8**                                                                                              | **V1**                                                             | **Comments**               |
|-----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|----------------------------|
| `POST`<br/>`/periodic-payments/{paymentProduct}`                                                    | `POST`<br/>`/periodic-payments/{paymentProduct}`                   | no changes in path         |
| `DELETE`<br/>`/periodic-payments/{paymentProduct}/{paymentId}`                                      | `DELETE`<br/>`/periodic-payments/{paymentProduct}/{paymentId}`     | no changes in path         |
| `GET`<br/>`/periodic-payments/{paymentProduct}/{paymentId}`                                         | `GET`<br/>`/periodic-payments/{paymentProduct}/{paymentId}`        | no changes in path         |
| `GET`<br/>`/periodic-payments/{paymentProduct}/{paymentId}/authorisations`                          | _removed from PIS_                                                 | moved to signing product   |
| `POST`<br/>`/periodic-payments/{paymentProduct}/{paymentId}/authorisations`                         | _removed from PIS_                                                 | moved to signing product   |
| `GET`<br/>`/periodic-payments/{paymentProduct}/{paymentId}/authorisations/`<br/>`{authorisationId}` | _removed from PIS_                                                 | moved to signing product   |
| `GET`<br/>`/periodic-payments/{paymentProduct}/{paymentId}/status`                                  | `GET`<br/>`/periodic-payments/{paymentProduct}/{paymentId}/status` | no changes in path         |
<br/>

---

### Headers
There are no changes in headers between V8 and V1

---
<br/>

### Request/Response body changes
#### Some new fields are added in V1 compared to V8. <br/> Removed fields are not marked in this release notes. <br/>You can see new request/response body samples bellow.

---
<br/>

### Creates a periodic payment initiation (POST /periodic-payments/{paymentProduct})
| **Request body V1 **                             | **Comments** |
|--------------------------------------------------|--------------|
| `templateId`                                     |              |
| `InstructedAmount.currency`                      |              |
| `InstructedAmount.amount`                        |              |
| `DebtorAccount.iban`                             |              |
| `DebtorAccount.bban`                             | new field    |
| `debtorAccountMessage`                           |              |
| `CreditorAccount.iban`                           |              |
| `creditorName`                                   |              |
| `requestedExecutionDate`                         |              |
| `remittanceInformationUnstructured`              |              |
| `RemittanceInformationStructured.reference`      |              |
| `RemittanceInformationStructured.referenceType`  |              |
| `startDate`                                      |              |
| `frequency`                                      |              |
<br/>

| **Response body V1 **                            | **Comments** |
|--------------------------------------------------|--------------|
| `paymentId`                                      |              |
| `templateId`                                     |              |
| `transactionStatus`                              | new field    |
| `instructedAmount.currency`                      |              |
| `instructedAmount.amount`                        |              |
| `debtorAccount.iban`                             |              |
| `debtorAccount.bban`                             | new field    |
| `debtorAccountMessage`                           |              |
| `creditorAccount.iban`                           |              |
| `creditorName`                                   |              |
| `requestedExecutionDate`                         |              |
| `remittanceInformationUnstructured`              |              |
| `remittanceInformationStructured.reference`      |              |
| `remittanceInformationStructured.referenceType`  |              |
| `link.Status.href`                               |              |
| `startDate`                                      |              |
| `frequency`                                      |              |
---
<br/>


### Get the payment initiation (GET /periodic-payments/{paymentProduct}/{paymentId})
| **Response body V1 **                           | **Comments** |
|-------------------------------------------------|--------------|
| `paymentId`                                     |              |
| `templateId`                                    |              |
| `instructedAmount.currency`                     |              |
| `instructedAmount.amount`                       |              |
| `debtorAccount.iban`                            |              |
| `debtorAccount.bban`                            | new field    |
| `debtorAccountMessage`                          |              |
| `creditorAccount.iban`                          |              |
| `creditorName`                                  |              |
| `requestedExecutionDate`                        |              |
| `remittanceInformationUnstructured`             |              |
| `remittanceInformationStructured.reference`     |              |
| `remittanceInformationStructured.referenceType` |              |
| `link.Status.href`                              |              |
---
<br/>

### Payment initiation status (GET /periodic-payments/{paymentProduct}/{paymentId}/status)
| **Response body V1 **                                                                                    | **Comments** |
|----------------------------------------------------------------------------------------------------------|--------------|
| `paymentId`                                                                                              |              |
| `transactionStatus`                                                                                      |              |
| `scaMethods.authenticationType` <br/>`scaMethods.authenticationMethodId` <br/> `scaMethods.explanation`  |              |
| `tppMessages`                                                                                            |              |
| `link.startAuthorisationWithAuthenticationMethodSelection.href`                                          |              |
---
<br/>

### Delete the payment initiation (DELETE /periodic-payments/{paymentProduct}/{paymentId})
| **Response body V1 ** | **Comments**  |
|-----------------------|---------------|
| `transactionStatus`   |               |           
| `link.status.href`    |               |
---
<br/>



