### Quote request and accept

An authenticated client can request a tradable quote and then accept it. Default quote validity is 20 seconds

**Quote request**

1. Client sends a quote request  
&nbsp;&nbsp;&nbsp;Example 1 and 2
2. Client provides the quote id of the quote to accept.  
&nbsp;&nbsp;&nbsp;Example 3

## Example 1: quote request - single leg

Customer wants to buy 1000 EUR and sell USD and wants the exchange to be done on 2022-10-04.

### POST Quote request

```
{
   "customer_id":"00332864770005",
   "leg_requests":[
      {
         "credit_currency":"EUR",
         "debit_currency":"USD",
         "tenor":"2022-10-04",
         "amount":{
            "amount":1000,
            "currency":"EUR"
         }
      }
   ]
}
```

### Response

The response contains among other things the exchange rate, the amount that will be exchanged, and the quote id which is used if the customer wants to accept the quote. *Note 1:* Accepting the quote is not required. *Note 2:* A quote is only valid for a certain time, indicated by the valid_until field.

In the response below, SEB offers the customer to buy 1000 EUR in exchange for 1165.94 USD.

```
{
   "transaction_id": "00000000-0000-0000-0000-000000000000",
   "valid_until":"2022-10-03T08:18:06.697442Z",
   "quote_id":"8c65af89-0b57-4910-b740-7450e07d8153",
   "customer_id":"00332864770005",
   "legs":[
      {
         "credit_amount":{
            "amount":1000.0,
            "currency":"EUR"
         },
         "debit_amount":{
            "amount":1165.94,
            "currency":"USD"
         },
         "exchange_rate":{
            "rate":1.165935,
            "forward_points":-6.5E-5,
            "rate_currency":"USD",
            "quoted_currency":"EUR"
         },
         "settlement_date":"2022-10-04",
         "regulatory_data":{
            
         }
      }
   ],
   "product_type":"OUTRIGHT",
   "status":"PENDING_ACCEPT"
}
```

## Example 2: quote request - multi leg (swap)

Customer wants to 
- Sell 1000 EUR and buy USD on SPOT (normally two business days after today's date).
- Sell 1000 EUR and buy USD on 1W (one week after SPOT).

### POST Quote request

```
{
   "customer_id":"00332864770005",
   "leg_requests":[
      {
         "credit_currency":"USD",
         "debit_currency":"EUR",
         "tenor":"SPOT",
         "amount":{
            "amount":1000,
            "currency":"EUR"
         }
      },
      {
         "credit_currency":"EUR",
         "debit_currency":"USD",
         "tenor":"1W",
         "amount":{
            "amount":1000,
            "currency":"EUR"
         }
      }
   ]
}
```

### Response

*Note* The tenors on the request (SPOT, 1W) have been translated to actual dates, 2022-10-05 and 2022-10-12 respectively, in the response.

```
{
   "valid_until":"2022-10-03T08:28:59.272982Z",
   "quote_id":"75b4b416-8fc7-4e34-99e4-251bb8b2b6c8",
   "customer_id":"00332864770005",
   "legs":[
      {
         "credit_amount":{
            "amount":1163.54,
            "currency":"USD"
         },
         "debit_amount":{
            "amount":1000.0,
            "currency":"EUR"
         },
         "exchange_rate":{
            "rate":1.16354,
            "rate_currency":"USD",
            "quoted_currency":"EUR"
         },
         "settlement_date":"2022-10-05",
         "regulatory_data":{
            "cfi_code":"SFCXXP",
            "isin":"EZ22QT9MWXN5",
            "executing_firm_lei":"F3JS33DEI6XQ4ZBPTN86"
         }
      },
      {
         "credit_amount":{
            "amount":1000.0,
            "currency":"EUR"
         },
         "debit_amount":{
            "amount":1164.01,
            "currency":"USD"
         },
         "exchange_rate":{
            "rate":1.164007,
            "forward_points":4.67E-4,
            "rate_currency":"USD",
            "quoted_currency":"EUR"
         },
         "settlement_date":"2022-10-12",
         "regulatory_data":{
            "cfi_code":"SFCXXP",
            "isin":"EZ22QT9MWXN5",
            "executing_firm_lei":"F3JS33DEI6XQ4ZBPTN86"
         }
      }
   ],
   "product_type":"SWAP",
   "status":"PENDING_ACCEPT"
}
```

### Example 3: Quote accept

If the customer wants to accept the quote, a POST is done to the quote accept endpoint. The response is very similar to the quote request response.

### POST Quote accept

```
Request body should be empty. 
```
### Response

```
{
   "transaction_id":"9fdd0f30-42f3-11ed-9150-dd8362dffb96",
   "quote_id":"8c65af89-0b57-4910-b740-7450e07d8153",
   "legs":[
      {
         "credit_amount":{
            "amount":1000.0,
            "currency":"EUR"
         },
         "debit_amount":{
            "amount":1165.94,
            "currency":"USD"
         },
         "exchange_rate":{
            "rate":1.165935,
            "forward_points":-6.5E-5,
            "rate_currency":"USD",
            "quoted_currency":"EUR"
         },
         "settlement_date":"2022-10-04",
         "regulatory_data":{
            
         }
      }
   ],
   "product_type":"OUTRIGHT"
}
```