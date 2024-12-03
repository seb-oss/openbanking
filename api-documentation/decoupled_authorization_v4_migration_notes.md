## New required parameters

The endpoints `POST /auth/v4/authorizations` and `GET /auth/v4/authorizations/:authorizationId` require that the TPP specifies the http header `psu-ip-address`.  
The header should contain the ip address of the PSU as seen from the TPP.

## Change of hint codes

Hint codes returned in field `hint_code` have been changed to better align with the official BankID documentation.  
As an example in v3 the hint_code `OUTSTANDING_TRANSACTION` was returned and v4 will instead return `outstandingTransaction`.  

You can find more information about BankIDs hint codes on the [BankID developer site](https://developers.bankid.com/api-references/auth--sign/collect)  
In addition there are a few SEB specific hint codes that can also be returned as follows (also described in the openapi specification)

|hint_code|description|
|--|--|
|sebTimeout|The authentication took too long and was cancelled by SEB|

__NOTE__ Your application must be able to handle unknown hint codes

## Changes in error response bodies

The error responses in v4 have been made more descriptive compared to v3, and more errors will now return specific error responses instead of "Internal server error".  
The type field now follows RFC9457 and contains a URI that can be used as a problem identifier for many specific problems, or 'about:blank'.  
Do note that these URIs __CAN NOT__ be dereferenced and should simply be used as identifiers.


v3 example
```
{
  "detail": null,
  "title": "The provided id has already been used to retrieve an access token",
  "status": 422,
  "type": "Invalid parameter value"
}
```

v4 example
```
  {
      "type": "https://authorize.sebgroup.com/problems/invalid-refresh-token",
      "title": "Invalid parameter value",
      "status": 400,
      "detail": "The provided refresh token is invalid",
      "instance": "/auth/v4/tokens"
  }
```


Refer to the OpenAPI specification for information regarding which errors can be returned from the different endpoints.

## Changes in error response http status code

Some error responses have changed http status code between v3 and v4, please refer to the table below

|Description|v3|v4|
|--|--|--|
|Calling tokens endpoint with reused or invalid refresh token|422|400|
|Calling tokens endpoint with invalid client id/secret|422|400|
|Calling tokens endpoint with invalid redirect uri|422|400|


## Documentation improvements
The following request parameters have been marked as mandatory

|Endpoint|Parameter|
|--|--|
|/auth/v4/authorizations|client_id|
|/auth/v4/authorizations|scope|
|/auth/v4/authorizations|start_mode|
|/auth/v4/tokens|redirect_uri|


These parameters were de-facto mandatory in v3, but were marked as optional in the openapi specification.
