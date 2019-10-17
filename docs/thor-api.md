---
id: thor api
title: Thor API
sidebar_label: Thor API
---

### Webhook Order Created

* **Method**: POST
* **URL**: 
  * Test: ```https://thorfunctionstest.azurewebsites.net/webhooks/{tenantId}/orders?code={token}```
  * Prod: ```https://thorfunctionsprod.azurewebsites.net/webhooks/{tenantId}/orders?code={token}```
* **Parameters**:
  * tenandId : [ faar | faco | facl | fape | soar | soco | socl | sope | somx ].
  * token: Authentication Token
* **Body**:

```json

{
  "event": "onOrderCreated",
  "payload":{
    "OrderId": 3272813
  }
} 
```
* **Response code**
  * 200 - Webhook successfully
  * 401 - Webhook Unauthorized

### Webhook Order Status Changed

* **Method**: POST
* **URL**: 
  * Test: ```https://thorfunctionstest.azurewebsites.net/webhooks/{tenantId}/orders/status?code={token}```
  * Prod: ```https://thorfunctionsprod.azurewebsites.net/webhooks/{tenantId}/orders/status?code={token}```
* **Parameters**:
  * tenandId : [ faar | faco | facl | fape | soar | soco | socl | sope | somx ].
  * token: Authentication Token
* **Body**:

```json
{
  "event":"onOrderItemsStatusChanged",
  "payload":{
    "OrderId":"1537945",
    "OrderItemIds":[
      "1300368",
      "1300369"
    ],
    "NewStatus":"canceled|ready_to_ship|shipped|delivered"
  }
}

```
* **Response code**
  * 200 - Webhook successfully
  * 401 - Webhook Unauthorized
  
### Webhook Product Created

* **Method**: POST
* **URL**: 
  * Test: ```https://thorfunctionstest.azurewebsites.net/webhooks/{tenantId}/products?code={token}```
  * Prod: ```https://thorfunctionsprod.azurewebsites.net/webhooks/{tenantId}/products?code={token}```
* **Parameters**:
  * tenandId : [ faar | faco | facl | fape | soar | soco | socl | sope | somx ].
  * token: Authentication Token
* **Body**:

```json
{
  "event": "onProductCreated",
  "payload": {
    "SellerSkus": [
      "881172242"
    ]
  }
}
```

* **Response code**
  * 200 - Webhook successfully
  * 401 - Webhook Unauthorized

###  API Webtracking Status

* **Method**: GET
* **URL**: 
  * Test: ```https://thorfunctionstest.azurewebsites.net/v1/orders/{internalOrderId}/status?code={token}/```
  * Prod: ```https://thorfunctionsprod.azurewebsites.net/v1/orders/{internalOrderId}/status?code={token}/```
* **Parameters**:
  * internalOrderId: internal order id
  * token: Authentication Token
* **Response code**
  * 200 - Webhook successfully
  * 401 - Request Unauthorized
  * 404 - Internal Order Id not found

### API Refund Product

* **Method**: POST
* **URL**: 
  * Test: ```https://thorfunctionstest.azurewebsites.net/v1/orders/{id}/refund?tenant={tenant_id}&code={token}```
  * Prod: ```https://thorfunctionsprod.azurewebsites.net/v1/orders/{id}/refund?tenant={tenant_id}&code={token}```
* **Parameters**:
  * id: internal order id
* **Query**:
  * tenandId : [ faar | faco | facl | fape | soar | soco | socl | sope | somx ].
  * token: Authentication Token
* **Body**:
  * action : ["SAME_PRODUCT" | "OTHER_PRODUCT" | "REFUND"]
```json
{
 "products": [
{
 "sku": "353629837",
 "quantity": 3
}],
 "action": "SAME_PRODUCT",
 "value": 234.12
}
```
