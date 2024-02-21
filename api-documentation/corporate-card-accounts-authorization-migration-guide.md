## Migration Guide for Corporate Authorization ##

The Corporate authorization flow grants access to the Corporate Card Account API for integration with your systems. Please note that this authorization flow does not grant you access to the private card account API.

We have separated the Corporate authorization flow from the private flow to simplify the integration and make it clearer what the different authorization flows grant access to.

Please refer to the [swagger](https://developer.sebgroup.com/products/psd2-branded-card-accounts/corporate-card-accounts-authorization) for detailed information about how to integrate your applications with our APIs.

Following is a brief migration guide for any application using our corporate card account API. Private authorization remains unchanged and will not require any adjustments on your end.

1. Redirect the user for authenticating with our API to a new subdomain on the same domain.
Our new URL is https://id.sebkort.com/cvo/ds/external/**brandId**/auth/tpplogin?client_id=`your_client_id`&response_type=code&scope=psd2_accounts%20psd2_payments&redirect_uri=**final_redirect_back_to_you**

2. Move the query parameter `brandId` and set it as a path parameter instead.
Set the `brandId` in the path and leave the `brandId` out of the query parameter list.

3. Adjust the names of corporate brands to the new naming standard.
- We've simplified the `brandIds` for corporate authorization, and thus this is required to be adjusted on your side as well.
You can find the updated names on our public GitHub [here](https://github.com/sebgroup/openbanking/blob/master/brandedcards/brandid.md)

Besides these three steps, the authorization flow will work as before, and no further adjustments are needed to continue using our corporate authorization flow.

If you have implemented the corporate authorization flow in any applications catering to individual customers, we urge you to remove this authorization method from them. 
The corporate authorization flow is made to grant access to the corporate API, which is used to list available accounts for company administrators and does not show the individual customers' corporate cards.
