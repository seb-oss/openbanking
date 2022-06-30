# SEB PSD2 Postman collection
Get started using SEBs PSD2 products with postman collection. Mocked data is available through sandbox apps. Real data is available through production apps.

Read [SEB Developer Portal](https://developer.sebgroup.com) for more information.

### Prerequisite
You need to have your own sandbox credentials to test this collection against our sandbox. Go to [SEB Developer Portal Apps](https://developer.sebgroup.com/apps) to retrieve client ID & client secret.  

## How to use SEB PSD2 Postman collection

### Step 1. Importing Collection into Postman
1. Open Postman
1. Select Import in the left navigation menu.
1. Select the files you want to import.
1. Select Import to bring your data into Postman.
 
### Step 2. Importing Environment into Postman
1. Click on the Environments tab on the left navbar of Postman
1. Click on the Import button
1. Click on the Upload Files button
1. Click on the Import Button
 
### Step 3. Set your own Environment  
1. Click on the Environments tab on the left navbar of Postman
2. Select 'SEB PSD2 Sandbox'
3. Add your own variables for below, leave others empty. You will find below values when you create sandbox App from developer portal.  

* clientId
* clientSecret
* redirectUri (should be same one used to create a sandbox app)

![Screenshot environment variables] (https://github.com/sebgroup/openbanking/blob/master/postman/images/postman_env.png)
 
4. In the top right corner of Postman, click the environment selector and select 'SEB PSD2 Sandbox'. 

Now you are ready to test.
 

## Authorization
The Authorization APIs provide for an authorization & authentication mechanism for SEBs APIs. These APIs are used to obtain security tokens for protected APIs. We offer the redirect and decoupled authorization and you can test both from our sandbox.
Read [PSD2 Authorization](https://developer.sebgroup.com/products/authorization) for more information.

### Redirect Authorization 
[Redirect Authorization step by step guide](https://developer.sebgroup.com/products/authorization/redirect-authorization) 

1. Request approval for an Authorization Code
Obtaining the authorization code is an interactive process, which requires you to log in as a user. ** It requires you to execute the request in the browser**   
  ``` 
  https://api-sandbox.sebgroup.com/mga/sps/oauth/oauth20/authorize?client_id={{clientId}}&scope=psd2_accounts&redirect_uri={{redirectUri}}&response_type=code&state=&brandid
  ``` 
You could find a uri to copy by clicking [Send] button from postman (look at the console window in the bottom)

Add your sandbox identity number, you can find a list of available identity number from [SEB Developer Portal](https://developer.sebgroup.com/products/authorization/redirect-authorization#/authorize-get):

![Screenshot redirect authorization] (https://github.com/sebgroup/openbanking/blob/master/postman/images/authorization.png)

You can find authorization code in your browser:

![Screenshot redirect authorization code] (https://github.com/sebgroup/openbanking/blob/master/postman/images/authorization_code.png)

2. Request access token for Authorization Code or Refresh Token
Add collected authorization code provided by the /authorize endpoint to body.

3. Use a token to access an API

### Decoupled Authorization 
[Decoupled Authorization step by step guide](https://developer.sebgroup.com/products/authorization/decoupled-authorization) 

1. Initiate authorization request
2. Check status
3. Bank ID simulation for sandbox  
4. Check status again to collect autostart_token
5. Retrieve access token

Now you are ready to call SEB PSD2 APIs with your access token.

 


