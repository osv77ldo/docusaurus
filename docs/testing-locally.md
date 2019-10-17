---
id: testing locally
title:  How to test locally
sidebar_label: How to test locally
---

### Pushing messages
--
**1. Run the command**

_Setup "isEncrypted"= false in local.settings.json and pull environment variables again._

```shell
$ npm run push:msg {topicName} {json filepath} {business}
```

Examples
```shell
$ npm run push:msg order.created order.json fa
$ npm run push:msg order.created order.json so
```
**2. Message Structure**

##### Id: 
* Needs to add a unique value (Verify that the value does not exist on database)
* Needs to start with `1`: FA `2`: SO **+** ar: `1`, co: `2`, cl: `3`, mx: `4`, pe: `5` **+** `OrderId`
* Example: Id: 131600032

##### TenantId: 
* Values: facl | socl | faco | soco | fape| sope | faar | soar | somx

##### Order.PromisedShippingTime
* Needs to be >= today

##### Order.BillingType
* Values: boleta | factura

##### Order.NationalRegistrationNumber
* Value required

##### OrderItems.OrderItemId
* Needs to add a unique value by item

##### OrderItems.Sku
* Needs to add a valid SKU

##### OrderItems.PromisedShippingTime
* Needs to be >= today


SKUs Data
--

#### FACL
| SKU | UPC  |
| ---------- | ---------- |
|1020393 ||
|880630138 |2998806301385|

<details>
  <summary>FACL SKU out of stock</summary>
<p>

| SKU| UPC|
| ------ | ------ |
| 4192519| 885370737882|
| 5564293| 8433886475877| 

</p></details>

#### FACO
| SKU| UPC|
| ------ | ------ |
|880280033| |
|1568772| |


#### FAPE
| SKU| UPC|
| ------ | ------ |
|13355096|2013355096008|
|14077330|2014077330005|
|14335993|2014335993003|
|14335994|2014335994000|
|14335995|2014335995007|
|14421691|2014421691004|
|14440639|2014440639001|
|14536992|2014536992003|
|14539852|2014539852007|
|14571155|2014571155005|
|14758095|2014758095001|
|14864157|2014864157006|
|14953467|2014953467009|
|15010589|2015010589009|
|15085834|2015085834004|
|15097778|2015097778006|
|15141615|2015141615004|
|15235640|2015235640004|
|15705952|2015705952002|
 
#### SOCL
| SKU | UPC  |
| ---------- | ---------- |
| 1264117  |1000071   |

#### SOMX
| SKU |  
| ----------  |
|2992|
|300X|
|3344|
|3018|
|3026|
|3034|
|3042|
|3050|
|3352|
|3069|
|3077|
|3360|
|3085|
|3093|
|3107|
|3379|


Checking order status 
--

* **invoiced:** order was successfully created and invoiced  :+1:  
* **canceled:** order does not have available stock :+1: 
* **pending:** order was not successfully created on FA|SO. (Payload error on OMS | Dadi) :\-1: 
* **failed:**  order was not successfully created on FA|SO. (Problems with back-office systems or Payload error on ASL| UXPOS) :\-1: 
* **allocated:** order was successfully created but not invoiced (Problems with back-office systems or Payload error) :\-1: 
* **invoiced_failed:**  order was not successfully invoiced on FA|SO. (Problems with back-office systems or Payload error):\-1: 

Examples:
--
#### Falabella Chile:

<details>
  <summary>Click to see example</summary>
<p>


```json
{
   "Id":"131600032", 
   "TenantId":"facl",
   "Order":{
      "OrderId":"1600032",
      "DeliveryOption": "ShipToAddress",
      "StoreId": "",
      "CustomerFirstName":"Paula",
      "CustomerLastName":"Castro Rojas",
      "OrderNumber":"100000039",
      "PaymentMethod":"CashOnDelivery_Payment",
      "Remarks":"",
      "DeliveryInfo":"",
      "Price":"11960.00",
      "GiftOption":"0",
      "GiftMessage":"",
      "VoucherCode":"",
      "BillingType":"boleta",
      "CreatedAt":"2018-12-13 14:28:17",
      "UpdatedAt":"2018-12-13 15:18:14",
      "AddressUpdatedAt":"2018-10-30 20:28:17",
      "AddressBilling":{
         "FirstName":"Paula",
         "LastName":"Castro Rojas",
         "Phone":"",
         "Phone2":"9 6754 7485",
         "Address1":"Las condes 1111 1111",
         "Address2":"",
         "Address3":"",
         "Address4":"",
         "Address5":"",
         "CustomerEmail":"paulascr@gmail.com",
         "City":"",
         "Ward":"",
         "Region":"",
         "PostCode":"",
         "Country":"Chile"
      },
      "AddressShipping":{
         "FirstName":"Paula",
         "LastName":"Castro Rojas",
         "Phone":"",
         "Phone2":"9 6754 7485",
         "Address1":"Las condes 1111, Int 111",
         "Address2":"LAS CONDES",
         "Address3":"",
         "Address4":"",
         "Address5":"",
         "CustomerEmail":"",
         "City":"Metropolitana, Las Condes",
         "Ward":"",
         "Region":"",
         "PostCode":"0013114",
         "Country":"Chile"
      },
      "NationalRegistrationNumber":"17.186.807-6",
      "ItemsCount":"1",
      "PromisedShippingTime":"2018-12-20 20:00:00",
      "ExtraAttributes":"",
      "Statuses":{
         "Status":"pending"
      }
   },
   "OrderItems":[
      	  {
         "OrderItemId":"1210001",
         "ShopId":"2037754",
         "OrderId":"1600032",
         "Name":"Pincel Acuarela Pelo de Ardilla",
         "Sku":"4989166",
         "Upc":"4548736027237",
         "Variation":"Talla Única",
         "ShopSku":"PL593OS1AT2J4LACL-4989166",
         "ShippingType":"Dropshipping",
         "ItemPrice":"3990.00",
         "PaidPrice":"3990.00",
         "Currency":"CLP",
         "WalletCredits":"0.00",
         "TaxAmount":"236.30",
         "CodCollectableAmount":"",
         "ShippingAmount":"1990.09",
         "ShippingServiceCost":"1990.09",
         "VoucherAmount":"0",
         "VoucherCode":"",
         "Status":"pending",
         "IsProcessable":"1",
         "ShipmentProvider":"Falabella",
         "IsDigital":"0",
         "DigitalDeliveryInfo":"",
         "TrackingCode":"",
         "TrackingCodePre":"",
         "Reason":"",
         "ReasonDetail":"",
         "PurchaseOrderId":"",
         "PurchaseOrderNumber":"",
         "PackageId":"",
         "PromisedShippingTime":"2018-12-18 20:00:00",
         "ExtraAttributes":"",
         "ShippingProviderType":"standard",
         "CreatedAt":"2018-12-13 14:28:17",
         "UpdatedAt":"2018-12-13 15:18:14",
         "ReturnStatus":""
	}
   ]
}
```

</p></details> 


#### Falabella Colombia:
<details>
  <summary>Click to see example</summary>
<p>


``` json
{
   "Id":"121700001",
   "TenantId":"faco",
   "Order":{
      "OrderId":"1700001",
      "CustomerFirstName":"Paula",
      "CustomerLastName":"Castro Rojas",
      "OrderNumber":"110000001",
      "PaymentMethod":"CashOnDelivery_Payment",
      "Remarks":"",
      "DeliveryInfo":"",
      "Price":"5980.00",
      "GiftOption":"0",
      "GiftMessage":"",
      "VoucherCode":"",
      "BillingType":"boleta",
      "CreatedAt":"2018-12-12 14:28:17",
      "UpdatedAt":"2018-12-12 15:18:14",
      "AddressUpdatedAt":"2018-10-30 20:28:17",
      "AddressBilling":{
         "FirstName":"Paula",
         "LastName":"Castro Rojas",
         "Phone":"",
         "Phone2":"9675474852",
         "Address1":"Av Bogota",
         "Address2":"",
         "Address3":"",
         "Address4":"",
         "Address5":"",
         "CustomerEmail":"paulascr@gmail.com",
         "City":"Bogota D.C",
         "Ward":"",
         "Region":"",
         "PostCode":"",
         "Country":"Colombia"
      },
      "AddressShipping":{
         "FirstName":"Paula",
         "LastName":"Castro Rojas",
         "Phone":"",
         "Phone2":"9675474852",
         "Address1":"Av Bogota",
         "Address2":"Bogota, Bogota D.C",
         "Address3":"",
         "Address4":"",
         "Address5":"",
         "CustomerEmail":"",
         "City":"Bogota, Bogota D.c, Bogota D.c",
         "Ward":"",
         "Region":"",
         "PostCode":"",
         "Country":"Colombia"
      },
      "NationalRegistrationNumber":"51571948",
      "ItemsCount":"1",
      "PromisedShippingTime":"2018-12-13 20:00:00",
      "ExtraAttributes":"",
      "Statuses":{
         "Status":"pending"
      }
   },
   "OrderItems":[
      {
         "OrderItemId":"6815908",
         "ShopId":"7297822",
         "OrderId":"1700001",
         "Name":"Lija Para Tacos - Generica",
         "Sku":"24380521",
         "Upc":"887961383249",
         "Variation":"",
         "ShopSku":"GE566SP0YBDCULCO-8922876",
         "ShippingType":"Dropshipping",
         "ItemPrice":"3990.00",
         "PaidPrice":"3990.00",
         "Currency":"CLP",
         "WalletCredits":"0.00",
         "TaxAmount":"236.30",
         "CodCollectableAmount":"",
         "ShippingAmount":"1990.09",
         "ShippingServiceCost":"1990.09",
         "VoucherAmount":"0",
         "VoucherCode":"",
         "Status":"pending",
         "IsProcessable":"1",
         "ShipmentProvider":"Falabella",
         "IsDigital":"0",
         "DigitalDeliveryInfo":"",
         "TrackingCode":"",
         "TrackingCodePre":"",
         "Reason":"",
         "ReasonDetail":"",
         "PurchaseOrderId":"",
         "PurchaseOrderNumber":"",
         "PackageId":"",
         "PromisedShippingTime":"2018-12-13 20:00:00",
         "ExtraAttributes":"",
         "ShippingProviderType":"standard",
         "CreatedAt":"2018-11-21 14:28:17",
         "UpdatedAt":"2018-11-21 15:18:14",
         "ReturnStatus":""
      }
   ]
}
```
</p></details> 

#### Sodimac Chile:
<details>
  <summary>Click to see example</summary>
<p>

```
{
   "Id":"231800018",
   "TenantId":"socl",
   "Order":{
      "OrderId":"1800018",
      "CustomerFirstName":"Paula",
      "CustomerLastName":"Castro Rojas",
      "OrderNumber":"220000019",
      "PaymentMethod":"CashOnDelivery_Payment",
      "Remarks":"",
      "DeliveryInfo":"",
      "Price":"19760.00",
      "GiftOption":"0",
      "GiftMessage":"",
      "VoucherCode":"",
      "BillingType":"boleta",
      "CreatedAt":"2018-12-13 14:28:17",
      "UpdatedAt":"2018-12-13 15:18:14",
      "AddressUpdatedAt":"2018-10-30 20:28:17",
      "AddressBilling":{
         "FirstName":"Paula",
         "LastName":"Castro Rojas",
         "Phone":"",
         "Phone2":"9 6754 7485",
         "Address1":"Manuel Antonio Tocornal 601 601",
         "Address2":"",
         "Address3":"",
         "Address4":"",
         "Address5":"",
         "CustomerEmail":"paulascr@gmail.com",
         "City":"",
         "Ward":"",
         "Region":"",
         "PostCode":"",
         "Country":"Chile"
      },
      "AddressShipping":{
         "FirstName":"Paula",
         "LastName":"Castro Rojas",
         "Phone":"",
         "Phone2":"9 6754 7485",
         "Address1":"Manuel Antonio Tocornal 601, Int 1702",
         "Address2":"SANTIAGO",
         "Address3":"",
         "Address4":"Esquina Argomedo",
         "Address5":"",
         "CustomerEmail":"",
         "City":"Metropolitana, Santiago",
         "Ward":"",
         "Region":"",
         "PostCode":"0013101",
         "Country":"Chile"
      },
      "NationalRegistrationNumber":"17.186.807-6",
      "ItemsCount":"4",
      "PromisedShippingTime":"2018-12-20 20:00:00",
      "ExtraAttributes":"",
      "Statuses":{
         "Status":"pending"
      }
   },
   "OrderItems":[
       {
         "OrderItemId":"1513650",
         "ShopId":"2190246",
         "OrderId":"1800014",
         "Name":"Lija Sev Pound It-Negro",
         "Sku":"1264117",
         "Upc":"6927700073438",
         "Variation":"...",
         "ShopSku":"SE759SP14S91WLACL-1264117",
         "ShippingType":"Dropshipping",
         "ItemPrice":"2350.00",
         "PaidPrice":"2350.00",
         "Currency":"CLP",
         "WalletCredits":"0.00",
         "TaxAmount":"375.30",
         "CodCollectableAmount":"",
         "ShippingAmount":"2590.09",
         "ShippingServiceCost":"1542.09",
         "VoucherAmount":"0",
         "VoucherCode":"",
         "Status":"pending",
         "IsProcessable":"1",
         "ShipmentProvider":"Blue Express",
         "IsDigital":"0",
         "DigitalDeliveryInfo":"",
         "TrackingCode":"",
         "TrackingCodePre":"",
         "Reason":"stock_out",
         "ReasonDetail":"Pruebas de integracion Falabella",
         "PurchaseOrderId":"",
         "PurchaseOrderNumber":"",
         "PackageId":"",
         "PromisedShippingTime":"2018-12-20 20:00:00",
         "ExtraAttributes":"",
         "ShippingProviderType":"standard",
         "CreatedAt":"2018-12-13 14:28:17",
         "UpdatedAt":"2018-12-13 15:18:14",
         "ReturnStatus":""
      },
	  {
        "OrderItemId":"1513651",
         "ShopId":"2190247",
         "OrderId":"1800014",
         "Name":"Lija Sev Pound It-Negro",
         "Sku":"475661",
         "Upc":"6927700073438",
         "Variation":"...",
         "ShopSku":"SE759SP14S91WLACL-475661",
         "ShippingType":"Dropshipping",
         "ItemPrice":"2350.00",
         "PaidPrice":"2350.00",
         "Currency":"CLP",
         "WalletCredits":"0.00",
         "TaxAmount":"375.30",
         "CodCollectableAmount":"",
         "ShippingAmount":"2590.09",
         "ShippingServiceCost":"1542.09",
         "VoucherAmount":"0",
         "VoucherCode":"",
         "Status":"pending",
         "IsProcessable":"1",
         "ShipmentProvider":"Blue Express",
         "IsDigital":"0",
         "DigitalDeliveryInfo":"",
         "TrackingCode":"",
         "TrackingCodePre":"",
         "Reason":"stock_out",
         "ReasonDetail":"Pruebas de integracion Falabella",
         "PurchaseOrderId":"",
         "PurchaseOrderNumber":"",
         "PackageId":"",
         "PromisedShippingTime":"2018-12-20 20:00:00",
         "ExtraAttributes":"",
         "ShippingProviderType":"standard",
         "CreatedAt":"2018-12-13 14:28:17",
         "UpdatedAt":"2018-12-13 15:18:14",
         "ReturnStatus":""
      },
	  {
         "OrderItemId":"1513652",
         "ShopId":"2190248",
         "OrderId":"1800014",
         "Name":"Lija Sev Pound It-Negro",
         "Sku":"475661",
         "Upc":"6927700073438",
         "Variation":"...",
         "ShopSku":"SE759SP14S91WLACL-475661",
         "ShippingType":"Dropshipping",
         "ItemPrice":"2350.00",
         "PaidPrice":"2350.00",
         "Currency":"CLP",
         "WalletCredits":"0.00",
         "TaxAmount":"375.30",
         "CodCollectableAmount":"",
         "ShippingAmount":"2590.09",
         "ShippingServiceCost":"1542.09",
         "VoucherAmount":"0",
         "VoucherCode":"",
         "Status":"pending",
         "IsProcessable":"1",
         "ShipmentProvider":"Blue Express",
         "IsDigital":"0",
         "DigitalDeliveryInfo":"",
         "TrackingCode":"",
         "TrackingCodePre":"",
         "Reason":"stock_out",
         "ReasonDetail":"Pruebas de integracion Falabella",
         "PurchaseOrderId":"",
         "PurchaseOrderNumber":"",
         "PackageId":"",
         "PromisedShippingTime":"2018-12-20 20:00:00",
         "ExtraAttributes":"",
         "ShippingProviderType":"standard",
         "CreatedAt":"2018-12-13 14:28:17",
         "UpdatedAt":"2018-12-13 15:18:14",
         "ReturnStatus":""
      },
	  {
        "OrderItemId":"1513653",
         "ShopId":"2190249",
         "OrderId":"1800014",
         "Name":"Lija Sev Pound It-Negro",
         "Sku":"475661",
         "Upc":"6927700073438",
         "Variation":"...",
         "ShopSku":"SE759SP14S91WLACL-475661",
         "ShippingType":"Dropshipping",
         "ItemPrice":"2350.00",
         "PaidPrice":"2350.00",
         "Currency":"CLP",
         "WalletCredits":"0.00",
         "TaxAmount":"375.30",
         "CodCollectableAmount":"",
         "ShippingAmount":"2590.09",
         "ShippingServiceCost":"1542.09",
         "VoucherAmount":"0",
         "VoucherCode":"",
         "Status":"pending",
         "IsProcessable":"1",
         "ShipmentProvider":"Blue Express",
         "IsDigital":"0",
         "DigitalDeliveryInfo":"",
         "TrackingCode":"",
         "TrackingCodePre":"",
         "Reason":"stock_out",
         "ReasonDetail":"Pruebas de integracion Falabella",
         "PurchaseOrderId":"",
         "PurchaseOrderNumber":"",
         "PackageId":"",
         "PromisedShippingTime":"2018-12-20 20:00:00",
         "ExtraAttributes":"",
         "ShippingProviderType":"standard",
         "CreatedAt":"2018-12-13 14:28:17",
         "UpdatedAt":"2018-12-13 15:18:14",
         "ReturnStatus":""
      }
   ]
}

```

</p></details> 

#### Sodimac México:
<details>
  <summary>Click to see example</summary>
<p>

```
{
  {
   "Id":"241900001",
   "TenantId":"somx",
   "Order":{
      "OrderId":"1900001",
      "DeliveryOption": "ShipToAddress",
      "CustomerFirstName":"Paula",
      "CustomerLastName":"Castro Rojas",
      "OrderNumber":"230000001",
      "PaymentMethod":"CashOnDelivery_Payment",
      "Remarks":"",
      "DeliveryInfo":"",
      "Price":"129.00",
      "GiftOption":"0",
      "GiftMessage":"",
      "VoucherCode":"",
      "BillingType":"boleta",
      "CreatedAt":"2019-01-20 14:28:17",
      "UpdatedAt":"2018-12-20 15:18:14",
      "AddressUpdatedAt":"2018-10-30 20:28:17",
      "AddressBilling": {
        "FirstName": "-",
        "LastName": "-",
        "Phone": "",
        "Phone2": "",
        "Address1": "-",
        "Address2": "-",
        "Address3": "",
        "Address4": "",
        "Address5": "",
        "CustomerEmail": "",
        "City": "-",
        "Ward": "",
        "Region": "",
        "PostCode": "-",
        "Country": "-"
      }
      "AddressShipping": {
              "FirstName": "Paula",
              "LastName": "Castro",
              "Phone": "",
              "Phone2": "",
              "Address1": "Hotel Marriot 333",
              "Address2": "Juárez, Cuauhtémoc",
              "Address3": "",
              "Address4": "(Hotel Marriot Reforma Habitacion 13)",
              "Address5": "",
              "CustomerEmail": "",
              "City": "Ciudad De México, Ciudad De México, Cuauhtémoc",
              "Ward": "",
              "Region": "",
              "PostCode": "06600",
              "Country": "Mexico"
      },
      "NationalRegistrationNumber":"76.212.492-0",
      "ItemsCount":"1",
      "PromisedShippingTime":"2018-12-23 20:00:00",
      "ExtraAttributes":"",
      "Statuses":{
         "Status":"pending"
      }
   },
   "OrderItems":[
       {
         "OrderItemId":"1513650",
         "ShopId":"2190246",
         "OrderId":"1800022",
         "Name":"PRUEBA MEXICO",
         "Sku":"2992",
         "Upc":"6927700073438",
         "Variation":"...",
         "ShopSku":"SE759SP14S91WLACL-2992",
         "ShippingType":"Dropshipping",
         "ItemPrice":"72.00",
         "PaidPrice":"72.00",
         "Currency":"MXN",
         "WalletCredits":"0.00",
         "TaxAmount":"3.30",
         "CodCollectableAmount":"",
         "ShippingAmount":"57.00",
         "ShippingServiceCost":"42.09",
         "VoucherAmount":"0",
         "VoucherCode":"",
         "Status":"pending",
         "IsProcessable":"1",
         "ShipmentProvider": "Estafeta",
         "IsDigital":"0",
         "DigitalDeliveryInfo":"",
         "TrackingCode":"",
         "TrackingCodePre":"",
         "Reason":"stock_out",
         "ReasonDetail":"Pruebas de integracion Falabella",
         "PurchaseOrderId":"",
         "PurchaseOrderNumber":"",
         "PackageId":"",
         "PromisedShippingTime":"2019-01-03 20:00:00",
         "ExtraAttributes":"",
         "ShippingProviderType":"standard",
         "CreatedAt":"2018-12-13 14:28:17",
         "UpdatedAt":"2018-12-13 15:18:14",
         "ReturnStatus":""
      }
   ]
}

```

</p></details> 

