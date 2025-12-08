# Signing External API - Release Notes

## Version 1.0.0

### Features and enhancements

The payment signing functionality has been moved from the PSD2 PIS API to a new signing API. This will increase
flexibility by enabling the same endpoint to handle the signing of one or multiple payments, or even a basket of
payments.

In January, we will send out more information regarding the new signing API and deploy a signing sandbox.

#### New endpoints

- `POST /signing-orders`: Initiates the signing of an order.
- `GET /signing-orders/{authorisationId}`: Get the status of an ongoing signing order.

### Migration notes

**Signing External API 1.0.0** is not compatible
with [Payment Initiation API 8.0.0](https://developer.sebgroup.com/products/psd2-payment-initiation/payment-initiation),
but it offers replacements for the following endpoints:

| Payment Initiation API 8.0.0                                                  | Signing External API 1.0.0              | Comments                                                                                                                                                                                                                                                                                                                                                                                          |
|:------------------------------------------------------------------------------|:----------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `GET /payments/{paymentProduct}/{paymentId}/authorisations`                   | N/A                                     | Removed with no replacement.                                                                                                                                                                                                                                                                                                                                                                      |
| `POST /payments/{paymentProduct}/{paymentId}/authorisations`                  | `POST /signing-orders`                  | **Request**:<ul><li>`paymentId` moved to the body.</li><li>`paymentProduct` is not used any longer.</li><li>Possible to provide multiple payment ids via `orderIds`.</li></ul>**Response**: <ul><li>`tppMessages`structure has changed.</li><li>`chosenScaMethod` has been renamed to `scaMethod` and includes new fields.</li><li>`paymentIds` is renamed to `orderIds`.</li></ul>               |
| `GET /payments/{paymentProduct}/{paymentId}/authorisations/{authorisationId}` | `GET /signing-orders/{authorisationId}` | **Request**:<ul><li> Only `authorisationId` is used in the path, and `paymentProduct` and `paymentId` are no longer needed.</li></ul>**Response**: <ul><li>`tppMessages`structure has changed.</li><li>`chosenScaMethod` has been renamed to `scaMethod` and includes new fields.</li><li>`scaStatus` defines an enum with valid values.</li><li>`paymentIds` is renamed to `orderIds`.</li></ul> |
| `POST /signing-baskets/{basketId}/authorisations`                             | `POST /signing-orders`                  | **Request**:<ul><li>`basketId` moved to the body.</li></ul>**Response**: <ul><li>`tppMessages`structure has changed.</li><li>`chosenScaMethod` has been renamed to `scaMethod` and includes new fields.</li></ul>                                                                                                                                                                                 |
| `GET /signing-baskets/{basketId}/authorisations/{authorisationId}`            | `GET /signing-orders/{authorisationId}` | **Request**:<ul><li>`basketId` is not used any longer.</li></ul>**Response**: <ul><li>`tppMessages`structure has changed.</li><li>`chosenScaMethod` has been renamed to `scaMethod` and includes new fields.</li><li>`scaStatus` defines an enum with valid values.</li></ul>                                                                                                                     |

#### Additional changes - ScaMethods

The handling for scaMethods `bankIdQr` and `bankIdSameDevice` has changed regarding the PSU already having an
ongoing bankid transaction in progress. In **Payment Initiation API 8.0.0** the API would return HTTP status `400` with
scaStatus `started`, and the field tppMessages containing the message `The PSU already had a separate signing transaction in progress. This signing transaction has
been cancelled. No new signing transaction has been started. Please ask the PSU to retry. Calling this endpoint again
will retry the operation`.

In **Signing External API 1.0.0**, the API will return HTTP status `200` with scaStatus failed in the same scenario (see
JSON example below), and the API consumer will have to call the `POST /signing-orders` endpoint again to start a new
signing transaction.

```json
{
  "authorisationId": "13c853a9-ed7d-4aa1-83a4-44e1b10a46f2",
  "scaStatus": "failed",
  "scaMethod": {
    "authenticationType": "PHOTO_OTP",
    "authenticationMethodId": "bankIdQr",
    "name": "Mobilt BankId with QR-code",
    "explanation": "Mobilt BankId with QR-code scanning",
    "methodType": "DECOUPLED"
  },
  "psuMessage": "En identifiering eller underskrift pågår redan för ditt personnummer. Försök igen.",
  "orderIds": [
    "019ae839-03ee-7999-a01b-9027fd471c74"
  ],
  "tppMessages": [
    {
      "category": "ERROR",
      "code": "ALREADY_IN_PROGRESS",
      "text": "A BankID signing transaction was already in progress for the PSU."
    }
  ],
  "_links": {}
}
```

#### Additional changes - Error responses

The error responses include the following changes (see examples below):

1. Error responses include the new field `status`.
2. The value of the field `type` has changed.
3. The field `type` may contain the value `about:blank` in cases where there is no more specific information about the
   error than what is already communicated by the HTTP status code. The API consumer must be able to handle unknown
   values for the field `type`.

##### Example error responses

**Payment Initiation API 8.0.0**:

```json
{
  "title": "The addressed resource is unknown relative to the TPP",
  "detail": "Referenced path resource not found",
  "type": "https://berlingroup.com/error-codes/RESOURCE_UNKNOWN",
  "code": "RESOURCE_UNKNOWN"
}
```

**Signing External API 1.0.0**:

```json
{
  "type": "https://sign.seb.se/error-codes/RESOURCE_UNKNOWN",
  "title": "The addressed resource is unknown relative to the API Client.",
  "detail": "The provided authorisationId is unknown",
  "status": 404,
  "code": "RESOURCE_UNKNOWN"
}
```

### Known issues

None detected.
