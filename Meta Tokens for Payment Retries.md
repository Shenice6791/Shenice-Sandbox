# Meta Tokens for Payment Retries

Resources:
https://github.com/Renda02/Retrying-payments-with-Meta-Tokens?tab=readme-ov-file#doc-4242-document-payment-retries-using-meta-tokens

# DOC-4242 Document payment retries using Meta Tokens

With Meta Tokens, you can collect existing tokens from shoppers, ranked by their chances of completing a successful transaction. Using this method, you can try payment with the highest-ranking token, and if it fails, you can retry payment with the second-ranking token. In addition, this allows you to share tokens across multiple shops under the same company.

Because we care about safeguarding our customer's data, we tokenize their PAN number (Payment Account Number - the 16-18 digits on the front of their credit or debit card). With tokenized payments, the PAN is not transmitted during the transaction, making the payment more secure.

Tokenization is a process of replacing sensitive data with non-sensitive data.

A metatoken is a collection of the shopper's existing tokens (possibly across different shops) for the same shopper, ordered based on how likely they will lead to successful payment.

### Benefits of tokenization

- Increase revenues for businesses, especially those with subscription models.
- Let users share across multiple shops under the same company.
- Offer more secure payment. 
- Reuse of meta-token in retried payment. 

To secure your payment, you can tokenize payments with payment API, Application Programming Interface requests in which a token substitutes the PAN.

In the following API reference, you will find information on interacting with available endpoints. 

### Authentication

Each request to the meta-token must include an API KEY. Set this key to the x-api-key header value, for example:

```
curl https://checkout-test.adyen.com/v68/metaTokens \
-H 'x-api-key: ' \
-H 'content-type: application/JSON \
…
```
### Versioning

The version suffix has the following format: "vXX," where XX is the version number. 

For example:

`` https://checkout-test.adyen.com/v68/metaTokens `` 

### Endpoints

<details close>
<summary><b>POST</b>/metaTokens</summary>
<br>
Create a meta-token for Merchant requests with this endpoint.

#### Request parameters 
  
Request Item     | 	Data type| Required /Optional     |
| :---        |    :----:   |          ---: |
| shopperReference      | String       |Required  |
| merchantAccount  | String        | Required     |
  
#####   Sample Request 
  ```
  curl https://checkout-test.adyen.com/v68/metaTokens \
-H 'x-api-key: ' \
-H 'content-type: application/json' \
-d '{
"shopperReference": "shopper-123",
"merchantAccount": "YOUR_MERCHANT_ACCOUNT"
}'
  ```

#### Response parameters 
   
Response Item     | 	Data type| Required /Optional     |
| :---        |    :----:   |          ---: |
| shopperReference      | String       |Required  |
| merchantAccount  | String        | Required     |
| metaTokenId   | String           | Required     | 

##### Sample response

  ```
  {
"merchantAccount": "YOUR_MERCHNAT_ACCOUNT",
"shopperReference": "yourShopperReference",
"metaTokenId": "9647-2876"
}

```

> Creating the token might take you a couple of minutes and sometimes even up to half an hour.
  
</details>

<details close>
  <summary><b>POST</b>/payments</summary>
<br>
Make a meta-token payment with a metaTokenId.
  
#### Parameters 
  
##### Path parameters
  
  Path parameter     | 	Description|
  | :---        |    :----  |  
  |  metaTokenId      | When making a payment request with a MetaToken, you must include the metaTokenId.      |
 
</details>


### Reponse handling

After submitting the API call to MetaToken, you receive a response to inform the status that the request was received and processed. For example, depending on the status message of MetaToken, you may receive the following webhook notification. 

#### Response handling parameters 
<details close>
 <summary><h4>Success parameters </h4></summary>
  
Success Item     | 	Data type| MetaToken status    | Notes |
| :---        |    :----:   |          ---: |     :---   |
|  metaTokenId      | String       | unique Id  | The unique Id is only generated to a metatoken successfully created.     |
| success  | String        | true   |    A metatoken has been created successfully.     |

##### Success webhook notification

```
{
"live": "false",
"notificationItems": [ {
"NotificationRequestItem": {
"merchantAccount": "YOUR_MERCHNAT_ACCOUNT"
"eventCode": "META_TOKEN_CREATION",
"metaTokenId": "9647-2876",
"success": "true"
}} ]}
```
</details>
<details close>
 <summary><h4>Error parameters </h4></summary> 

Error Item     | 	Data type| MetaToken status    | Notes |
| :---        |    :----:   |          ---: |     :---   |
| reason       | String       | Technical error  | The meta-token cannot be generated. </br> Send the request again.   |
| success  | String        | false   |    A metatoken has not been created successfully.     |

##### Error webhook notification

```
{ "live": "false",
"notificationItems": [
{
"NotificationRequestItem": {
"eventCode": "META_TOKEN_CREATION",
"reason": "Technical error",
"success": "false"
}}]}
```
</details>

##### **List of questions that I asked when documenting the feature.**

1. What is the difference between "metatoken" and "meta-token" naming on the document provided?
2. Do I need a merchant account? 
3. Where can I get api key? Is a quick guide needed to provide API keys? 
4. Can you point me to the information about the description of the parameters?
5. How are code snippets samples in a document tested?
