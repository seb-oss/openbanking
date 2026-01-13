# Private payment initiation changes from V8 to V1 condensed version

## Description of changes
Payment initiation (PIS v8) flow was separated to private and corporate, 
this changes is acceptable for private flow only.
---
<br/>

### URLs
| **V8**                                                  | **V1**                                                         |
|---------------------------------------------------------|----------------------------------------------------------------|
| `https://tpp-api.sebgroup.com/tpp/pis/v8/identified2/`  | `https://tpp-api.sebgroup.com/tpp/pis/private/v1/identified2/` |
| `https://api-sandbox.sebgroup.com/pis/v8/identified2/`  | `https://api-sandbox.sebgroup.com/pis/private/v1/identified2/` |
---
<br/>

### PATHs
| **V8**                                                                                     | **V1**                                                    | **Comments**               |
|--------------------------------------------------------------------------------------------|-----------------------------------------------------------|----------------------------|
| `PATCH`<br/>`/payments/mock/resetall`                                                      | `PATCH`<br/>`/payments/mock/resetall`                     | no changes in path         |
| `POST`<br/>`/payments/{paymentProduct}`                                                    | `POST`<br/>`/payments/{paymentProduct}`                   | no changes in path         |
| `DELETE`<br/>`/payments/{paymentProduct}/{paymentId}`                                      | `DELETE`<br/>`/payments/{paymentProduct}/{paymentId}`     | no changes in path         |
| `GET`<br/>`/payments/{paymentProduct}/{paymentId}`                                         | `GET`<br/>`/payments/{paymentProduct}/{paymentId}`        | no changes in path         |
| `GET`<br/>`/payments/{paymentProduct}/{paymentId}/authorisations`                          | _removed from PIS_                                        | moved to signing product   |
| `POST`<br/>`/payments/{paymentProduct}/{paymentId}/authorisations`                         | _removed from PIS_                                        | moved to signing product   |
| `GET`<br/>`/payments/{paymentProduct}/{paymentId}/authorisations/`<br/>`{authorisationId}` | _removed from PIS_                                        | moved to signing product   |
| `GET`<br/>`/payments/{paymentProduct}/{paymentId}/status`                                  | `GET`<br/>`/payments/{paymentProduct}/{paymentId}/status` | no changes in path         |
| `POST`<br/>`/signing-baskets`                                                              | `POST`<br/>`/signing-baskets`                             | no changes in path         |
| `GET`<br/>`/signing-baskets/{basketId}`                                                    | `GET`<br/>`/signing-baskets/{basketId}`                   | no changes in path         |
| `POST`<br/>`/signing-baskets/{basketId}/authorisations`                                    | _removed from PIS_                                        | moved to signing product   |
| `GET`<br/>`/signing-baskets/{basketId}/authorisations/`<br/>`{authorisationId}`            | _removed from PIS_                                        | moved to signing product   |
---
<br/>

### HTTP request/response Headers

#### There are no changes in headers between V8 and V1

---
<br/>

### Request/Response body changes
#### Some new fields are added in V1 compared to V8. <br/> Removed fields are not marked in this release notes. <br/>You can see new request/response body samples bellow.

---
<br/>

### Creates a payment initiation (POST /payments/{paymentProduct})
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
<br/>

| **Response body V1 **                           | **Comments** |
|-------------------------------------------------|--------------|
| `paymentId`                                     |              |
| `templateId`                                    |              |
| `transactionStatus`                             | new field    |
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

### Get the payment initiation (GET /payments/{paymentProduct}/{paymentId})
| **Response body V1 **                           | **Comments** |
|-------------------------------------------------|--------------|
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

### Payment initiation status (GET /payments/{paymentProduct}/{paymentId}/status)
| **Response body V1 **                                                                                    | **Comments** |
|----------------------------------------------------------------------------------------------------------|--------------|
| `paymentId`                                                                                              |              |
| `transactionStatus`                                                                                      |              |
| `scaMethods.authenticationType` <br/>`scaMethods.authenticationMethodId` <br/> `scaMethods.explanation`  |              |
| `tppMessages`                                                                                            |              |
| `link.startAuthorisationWithAuthenticationMethodSelection.href`                                          |              |
---
<br/>

### Delete the payment initiation (DELETE /payments/{paymentProduct}/{paymentId})
| **Response body V1 ** | **Comments**  |
|-----------------------|---------------|
| `transactionStatus`   |               |           
| `link.status.href`    |               |
---
<br/>

### Creates a signing basket (POST /signing-baskets)
| **Request body V1 ** | **Comments** |
|----------------------|--------------|
| `paymentIds`         |              |

| **Response body V1 **                                            | **Comments** |
|------------------------------------------------------------------|--------------|
| `paymentIds`                                                     |              |
| `transactionStatus`                                              |              |
| `basketId`                                                       |              |
| `links.status.href`                                              |              |
| `links.startAuthorisationWithAuthenticationMethodSelection.href` |              |
---
<br/>


### Get a signing basket (GET /signing-baskets/{basketId})

| **Response body V1 **                                            | **Comments** |
|------------------------------------------------------------------|--------------|
| `paymentIds`                                                     |              |
| `transactionStatus`                                              |              |
| `basketId`                                                       |              |
| `scaMethods.authenticationType`                                  |              |
| `scaMethods.authenticationMethodId`                              |              |
| `scaMethods.name`                                                |              |
| `scaMethods.explanation`                                         |              |
| `links.status.href`                                              |              |
| `links.startAuthorisationWithAuthenticationMethodSelection.href` |              |
---
<br/>
