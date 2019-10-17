---
id: message bus
title: Message Bus
sidebar_label: Message Bus
---

Service Bus topics and subscriptions support a publish/subscribe messaging communication model. When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.

Service Bus topics and subscriptions enable you to scale and process a large number of messages across many users and applications.

### Topics
<table style="font-size:12px;">
<tr>
    <th width="10%">TOPIC</th>
    <th width="10%">SUBSCRIPTION</td>
    <th width="50%">MESSAGE PROPERTIES</th>
    <th width="30%">EXAMPLE</th>
</tr>
<tr>
    <td>LINIO.ORDER.CREATED</td>
    <td><ul><li>linio.order </li></ul></td>
    <td><b>body</b>
      <ul>
      <li>Id: Tenant + Seller Center Order Id</li>
      <li>OrderId: Seller Center Order Id</li>
      <li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
    </ul>
    <b>brokerProperties</b>
    <ul>
    <li>CorrelationId: business [fa|so]</li>
    </ul>
    </td>
    <td><details><summary>Click</summary>
<p>

```json
{
  "Id": 1312345,
  "OrderId": 12345,
  "TenantId": "facl",
  "Business": "fa"
}
```
</p></details></td></tr>

<tr>
<td>LINIO.ORDER.CANCELED</td>
<td><ul><li>fa.order</li> <li>db.write</li></ul></td>
<td>
<b>body</b>
<ul>
<li>Id: Tenant + Seller Center Order Id</li>
<li>OrderId: Seller Center Order Id</li>
<li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
        <li>OrderItemIds: Seller Center Order Items Ids</li>
      </ul>
      <b>brokerProperties</b>
    <ul>
    <li>CorrelationId: Tenant </li>
    </ul>
    </td>
 <td><details><summary>Click</summary>
<p>

```json
  {
    "Id":"131537945",
    "OrderId":"1537945",
    "OrderItemIds":[
        "1300368",
        "1300369"
    ],
    "TenantId": "facl"
  }
```

</p></details></td></tr>

<tr>
    <td>ORDER.VALIDATED</td>
    <td><ul><li>fa.order</li><li>so.order</li><li>db.write</li></ul></td>
    <td><b>body</b>
    <ul>
     <li>Id: Tenant + Seller Center Order Id</li>
     <li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
     <li>Order: Seller Center Order Information</li>
    <li>OrderItemIds: Seller Center Order Items Ids</li>
    </ul>
    <b>brokerProperties</b>
    <ul>
    <li>CorrelationId: business [fa|so]</li>
    </td>
    <td>
<details>
  <summary>Click</summary>
<p>

```json
{
    "Id":"131600790", 
    "TenantId":"facl",
    "ShipmentProvider":"Falabella",
    "Order":{
       "OrderId":"1600790",
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
          "Sku":"1020393",
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

</p></details></td></tr>

<tr>
    <td>ORDER.CREATED</td>
    <td><ul><li>fa.order</li><li>so.order</li><li>db.write</li></ul></td>
    <td><b>body</b>
    <ul>
     <li>Id: Tenant + Seller Center Order Id</li>
     <li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
     <li>Order: Seller Center Order Information</li>
    <li>OrderItemIds: Seller Center Order Items Ids</li>
    </ul>
    <b>brokerProperties</b>
    <ul>
    <li>CorrelationId: business [fa|so]</li>
    </td>
    <td>
<details>
  <summary>Click</summary>
<p>

```json
{
  "Id": "131512862",
  "TenantId": "facl",
  "Order":{
      "OrderId":"1512862",
      "CustomerFirstName":"Test",
      "CustomerLastName":"Test",
      "DeliveryInfo":"STS_1234",
      "DeliveryOption":"ShipToStore",
      "StoreId": "1234",
      "OrderNumber":"206569766",
      "PaymentMethod":"CashOnDelivery_Payment",
      "Remarks":"",
      "DeliveryInfo":"",
      "Price":"5070.00",
      "GiftOption":"0",
      "GiftMessage":"",
      "VoucherCode":"",
      "CreatedAt":"2018-09-03 14:52:48",
      "UpdatedAt":"2018-09-03 14:52:48",
      "AddressUpdatedAt":"2018-09-03 17:52:48",
      "BillingType": "boleta",
      "AddressBilling":{
         "FirstName":"Test",
         "LastName":"Test",
         "Phone":"",
         "Phone2":"",
         "Address1":"Santiago 123",
         "Address2":"",
         "Address3":"",
         "Address4":"",
         "Address5":"",
         "CustomerEmail":"",
         "City":"METROPOLITANA",
         "Ward":"",
         "Region":"",
         "PostCode":"0013101",
         "Country":"Chile"
      },
      "AddressShipping":{
         "FirstName":"Test",
         "LastName":"Test",
         "Phone":"",
         "Phone2":"",
         "Address1":"Santiago 123",
         "Address2":"SANTIAGO",
         "Address3":"",
         "Address4":"",
         "Address5":"",
         "CustomerEmail":"",
         "City":"Metropolitana, Santiago",
         "Ward":"",
         "Region":"",
         "PostCode":"0013101",
         "Country":"Chile"
      },
      "NationalRegistrationNumber":"55.555.555-0",
      "ItemsCount":"1",
      "PromisedShippingTime":"2018-09-10 14:00:00",
      "ExtraAttributes":"",
      "Statuses":{
         "Status":"pending"
      }
   },
   "OrderItems":[
      {
         "OrderItemId":"1226509",
         "ShopId":"2012387",
         "OrderId":"1512862",
         "Name":"Pincel Acuarela",
         "Sku":"24SQI/01",
         "Upc": "123456",
         "Variation":"Talla Única",
         "ShopSku":"PL593OS0IVU9CLACL-5872078",
         "ShippingType":"Dropshipping",
         "ItemPrice":"1480.00",
         "PaidPrice":"1480.00",
         "Currency":"CLP",
         "WalletCredits":"0.00",
         "TaxAmount":"236.30",
         "CodCollectableAmount":"",
         "ShippingAmount":"3590.00",
         "ShippingServiceCost":"3574.09",
         "VoucherAmount":"0",
         "VoucherCode":"",
         "Status":"pending",
         "IsProcessable":"1",
         "ShipmentProvider":"Blue Express",
         "IsDigital":"0",
         "DigitalDeliveryInfo":"",
         "TrackingCode":"",
         "TrackingCodePre":"",
         "Reason":"",
         "ReasonDetail":"",
         "PurchaseOrderId":"",
         "PurchaseOrderNumber":"",
         "PackageId":"",
         "PromisedShippingTime":"2018-09-10 14:00:00",
         "ExtraAttributes":"",
         "ShippingProviderType":"express",
         "CreatedAt":"2018-09-03 14:52:48",
         "UpdatedAt":"2018-09-03 17:52:48",
         "ReturnStatus":""
      }
   ]
}
```

</p></details></td></tr>

<tr>
    <td>ORDER.FAILED</td>
    <td><ul><li>db.write</li><li>alert</li><li>cancel</li></ul></td>
    <td><b>body</b>
    <ul>
     <li>Id: Tenant + Seller Center Order Id</li>
      <li>OrderId: Seller Center Order Id</li>
      <li>Service: name of the service requested [ASL|OMS|DADI|UXPOS] </li>
      <li>Status: Order status [failed|invoiced_failed] </li>
      <li>Input: Input payload of the service requested</li>
      <li>Output: Response of the service requested</li>
<li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
    </ul>
    </td>
    <td>
<details>
  <summary>Click</summary>
<p>

```json
{
   "Id":"131512862",
   "OrderId":"1512862",
   "Service": "OMS",
   "TenantId": "facl",
   "Status": "failed",
   "Input": "{}",
   "Output": "{}"
}
```

</p></details></td></tr>
<tr>
    <td>ORDER.CANCELED</td>
    <td><ul>
    <li>linio.order</li> <li>db.write</li></ul></td>
    <td><b>body</b>
    <ul>
      <li>Id: Tenant + Seller Center Order Id</li>
      <li>OrderId: Seller Center Order Id</li>
      <li>OrderItemIds: Seller Center Order Item Id</li>
      <li>Reason: reason of cancelations </li>
      <li>Input: Input payload of the service requested</li>
      <li>Output: Response of the service requested</li>
      <li>Service: name of the service requested [ASL|OMS|DADI|UXPOS] </li>
      <li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
    </ul></td><td>
<details>
  <summary>Click</summary>
<p>


```json
{
  "Id": "11550163",
  "OrderId": "1550163",
  "OrderItemIds": ["1317020"],
  "Reason": "No se tiene el producto (Stock out)",
  "TenantId": "socl",
  "Input": "input",
  "Output": "output",
  "Service": "DADI"
}
```

</p></details></td></tr>

<tr>
    <td>FA.OMS.ORDER.CREATED</td>
    <td>
    <ul><li>fa.order</li><li>db.write</li></ul></td>
    <td><b>body</b>
    <ul>
     <li>Id: Tenant + Seller Center Order Id</li>
<li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
     <li>Order: Seller Center Order Information</li>
    <li>OrderItemIds: Seller Center Order Items Ids</li>
      <li>OmsOrder: OMS Output reponse</li>
    </ul><b>brokerProperties</b>
    <ul>
    <li>CorrelationId: business [fa|so]</li></td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
  "Id": "231512862",
  "TenantId": "facl",
  "Order": {
    "OrderId": "1512862",
    "CustomerFirstName": "Test",
    "CustomerLastName": "Test",
    "DeliveryInfo":"STS_1234",
    "DeliveryOption":"ShipToStore",
    "StoreId": "1234",
    "OrderNumber": "206569766",
    "PaymentMethod": "CashOnDelivery_Payment",
    "Remarks": "",
    "DeliveryInfo": "",
    "Price": "5070.00",
    "GiftOption": "0",
    "GiftMessage": "",
    "VoucherCode": "",
    "CreatedAt": "2018-09-03 14:52:48",
    "UpdatedAt": "2018-09-03 14:52:48",
    "AddressUpdatedAt": "2018-09-03 17:52:48",
    "AddressBilling": {
      "FirstName": "Test",
      "LastName": "Test",
      "Phone": "",
      "Phone2": "",
      "Address1": "Santiago 123",
      "Address2": "",
      "Address3": "",
      "Address4": "",
      "Address5": "",
      "CustomerEmail": "",
      "City": "METROPOLITANA",
      "Ward": "",
      "Region": "",
      "PostCode": "0013101",
      "Country": "Chile"
    },
    "AddressShipping": {
      "FirstName": "Test",
      "LastName": "Test",
      "Phone": "",
      "Phone2": "",
      "Address1": "Santiago 123",
      "Address2": "SANTIAGO",
      "Address3": "",
      "Address4": "",
      "Address5": "",
      "CustomerEmail": "",
      "City": "Metropolitana, Santiago",
      "Ward": "",
      "Region": "",
      "PostCode": "0013101",
      "Country": "Chile"
    },
    "NationalRegistrationNumber": "55.555.555-5",
    "ItemsCount": "1",
    "PromisedShippingTime": "2018-09-10 14:00:00",
    "ExtraAttributes": "",
    "Statuses": {
      "Status": "pending"
    },
    "BillingType": "boleta"
  },
  "OrderItems": [
    {
      "OrderItemId": "1226509",
      "ShopId": "2012387",
      "OrderId": "1512862",
      "Name": "Pincel Acuarela",
      "Sku": "24SQI/01",
      "Upc": "123456",
      "Variation": "Talla Única",
      "ShopSku": "PL593OS0IVU9CLACL-5872078",
      "ShippingType": "Dropshipping",
      "ItemPrice": "1480.00",
      "PaidPrice": "1480.00",
      "Currency": "CLP",
      "WalletCredits": "0.00",
      "TaxAmount": "236.30",
      "CodCollectableAmount": "",
      "ShippingAmount": "3590.00",
      "ShippingServiceCost": "3574.09",
      "VoucherAmount": "0",
      "VoucherCode": "",
      "Status": "pending",
      "IsProcessable": "1",
      "ShipmentProvider": "Blue Express",
      "IsDigital": "0",
      "DigitalDeliveryInfo": "",
      "TrackingCode": "",
      "TrackingCodePre": "",
      "Reason": "",
      "ReasonDetail": "",
      "PurchaseOrderId": "",
      "PurchaseOrderNumber": "",
      "PackageId": "",
      "PromisedShippingTime": "2018-09-10 14:00:00",
      "ExtraAttributes": "",
      "ShippingProviderType": "express",
      "CreatedAt": "2018-09-03 14:52:48",
      "UpdatedAt": "2018-09-03 17:52:48",
      "ReturnStatus": ""
    }
  ],
  "OmsOrder": {
    "OrderNumber": 5079056101,
    "OrderCreatedDate": "2018-09-05T14:26:02",
    "OrderCaptureDate": "2018-09-05T17:05:00",
    "ExternalOrderNumber": 1512867,
    "OrderSubtotal": 1480,
    "OrderTotal": 32390,
    "OrderCurrency": "CLP",
    "EnteredBy": "",
    "EnteredLocation": "",
    "EntryType": "",
    "Confirmed": true,
    "MinimizeShipments": false,
    "OrderType": "DTC",
    "OrderStatus": "DO Created",
    "LastUpdatedDTTM": "2018-09-05T14:26:03",
    "CustomerInfo": {
      "CustomerId": "55.555.555-5",
      "CustomerFirstName": "Test",
      "CustomerLastName": "Test",
      "CustomerPhone": "",
      "CustomerEmail": ""
    },
    "PaymentDetails": {
      "PaymentDetail": {
        "ExternalPaymentDetailId": 1,
        "PaymentMethod": "Others",
        "CardType": "",
        "AccountNumber": "",
        "AccountDisplayNumber": "",
        "NameAsOnCard": "",
        "CardExpiryMonth": "",
        "CardExpiryYear": "",
        "ReqAuthorizationAmount": 0,
        "ChargeSequence": 1,
        "ReferenceFields": {
          "ReferenceField1": "",
          "ReferenceField2": "",
          "ReferenceField4": "",
          "ReferenceField5": "",
          "ReferenceField6": "",
          "ReferenceField7": ""
        },
        "BillToDetail": {
          "BillToFirstName": "Test",
          "BillToLastName": "Test",
          "BillToAddressLine1": "Santiago 123",
          "BillToAddressLine2": "",
          "BillToAddressLine3": "",
          "BillToCity": "SANTIAGO CENTRO",
          "BillToState": 13,
          "BillToPostalCode": 366,
          "BillToCountry": "CL",
          "BillToPhone": "",
          "BillToEmail": ""
        }
      }
    },
    "ChargeDetails": {
      "ChargeDetail": {
        "ExtChargeDetailId": 144009841208,
        "ChargeCategory": "Misc",
        "ChargeName": "Shipping",
        "ChargeAmount": 30910
      }
    },
    "DiscountDetails": "",
    "Notes": "",
    "WMNotes": "",
    "ReferenceFields": {
      "ReferenceField1": "ATG",
      "ReferenceField2": "55.555.555-5",
      "ReferenceField3": "RUT"
    },
    "CustomFieldList": {
      "CustomField": [
        {
          "Name": "ActionType",
          "Value": ""
        },
        {
          "Name": "Email",
          "Value": ""
        },
        {
          "Name": "Error",
          "Value": ""
        },
        {
          "Name": "FirstName",
          "Value": ""
        },
        {
          "Name": "LastName",
          "Value": ""
        },
        {
          "Name": "Phone",
          "Value": ""
        },
        {
          "Name": "RUTID",
          "Value": ""
        },
        {
          "Name": "Relation",
          "Value": ""
        },
        {
          "Name": "TipoDoc",
          "Value": ""
        }
      ]
    },
    "WMProcessInfo": {
      "RefTextField1": 2000,
      "RefTextField2": "",
      "RefTextField3": "",
      "RefTextField4": "",
      "RefTextField5": "",
      "RefTextField6": ""
    },
    "OrderLines": {
      "OrderLine": {
        "LineNumber": 5950315,
        "OrderLineCreatedDate": "2018-09-05T14:26:02",
        "OrderLineStatus": "DO Created",
        "ItemID": 5950315,
        "ItemDescription": "RAYOVAC-@PILA ALCALINA",
        "LineTotal": 1480,
        "LastUpdatedDTTM": "2018-09-05T14:26:02",
        "PriceInfo": {
          "Price": 1480
        },
        "Quantity": {
          "OrderedQty": 1,
          "OrderedQtyUOM": "unit",
          "CancelledQty": 0,
          "TotalAllocatedQty": 1,
          "TotalCancelledQty": 0
        },
        "ShippingInfo": {
          "PromisedDeliveryBy": "2018-09-10T17:00:00",
          "RequestedDeliveryBy": "2018-09-10T17:00:00",
          "DesignatedServiceLevelCode": "AD",
          "ShipToFacility": "",
          "DeliveryOption": "Ship to address",
          "ShippingAddress": {
            "ShipToFirstName": "Test",
            "ShipToLastName": "Test",
            "ShipToAddressLine1": "Santiago 123",
            "ShipToAddressLine2": "",
            "ShipToAddressLine3": "",
            "ShipToCity": "SANTIAGO CENTRO",
            "ShipToState": 13,
            "ShipToPostalCode": 366,
            "ShipToCounty": "",
            "ShipToCountry": "CL",
            "ShipToPhone": "",
            "ShipToEmail": "",
            "ShipToFax": "",
            "ShipToLatitude": "",
            "ShipToLongitude": "",
            "ShipToVerifiedByAVS": false,
            "ShipToLocationType": ""
          }
        },
        "DiscountDetails": "",
        "ChargeDetails": "",
        "Notes": "",
        "WMNotes": {
          "WMNote": [
            {
              "NoteType": "DDate",
              "NoteCode": "",
              "CommentText": "2018-09-10T17:00:00.000Z"
            },
            {
              "NoteType": "LocldId",
              "NoteCode": "",
              "CommentText": 366
            },
            {
              "NoteType": "Region",
              "NoteCode": "",
              "CommentText": "REGION METROPOLITANA"
            },
            {
              "NoteType": "Comuna",
              "NoteCode": "",
              "CommentText": "SANTIAGO CENTRO"
            },
            {
              "NoteType": "Locality",
              "NoteCode": "",
              "CommentText": "SANTIAGO CENTRO"
            },
            {
              "NoteType": "SAddress",
              "NoteCode": "",
              "CommentText": "Santiago 123"
            },
            {
              "NoteType": "Ndoc",
              "NoteCode": "",
              "CommentText": "55.555.555-5"
            },
            {
              "NoteType": "TipoDoc",
              "NoteCode": "",
              "CommentText": "RUT"
            }
          ]
        },
        "LineReferenceFields": {
          "ReferenceField1": "",
          "ReferenceField2": false,
          "ReferenceField3": "AUTHORIZED",
          "ReferenceField4": "",
          "ReferenceField5": "AD",
          "ReferenceNumber1": "",
          "ReferenceNumber2": 0
        },
        "CustomFieldList": {
          "CustomField": [
            {
              "Name": "RUTID",
              "Value": ""
            },
            {
              "Name": "Relation",
              "Value": ""
            },
            {
              "Name": "Phone",
              "Value": ""
            },
            {
              "Name": "Email",
              "Value": ""
            },
            {
              "Name": "TipoDoc",
              "Value": ""
            },
            {
              "Name": "FirstName",
              "Value": ""
            },
            {
              "Name": "LastName",
              "Value": ""
            },
            {
              "Name": "ItemSubclass",
              "Value": ""
            }
          ]
        },
        "LineWMProcessInfo": {
          "LineRefTextField1": "",
          "LineRefTextField2": "",
          "LineRefTextField3": 144009841208,
          "LineRefTextField4": "",
          "LineRefTextField5": "",
          "LineRefTextField6": ""
        },
        "AllocationDetails": {
          "AllocationDetail": {
            "ItemID": 5950315,
            "AllocatedQuantity": 1,
            "AllocatedQtyUOM": "unit",
            "SupplyType": "OH",
            "SupplyID": "",
            "SupplyDetailID": "",
            "IsVirtualAllocation": false,
            "TierId": "Shipping Anywhere",
            "OriginFacilityAliasID": 2000,
            "FacilityType": "DC",
            "CommittedShipDTTM": "2018-09-09T18:45:00",
            "CommittedDeliveryDTTM": "2018-09-09T20:45:00",
            "MustReleaseByDTTM": "2018-09-06T21:00:00",
            "MustShipByDTTM": "2018-09-09T18:45:00",
            "CreatedDTTM": "2018-09-05T14:26:03",
            "ModifiedDTTM": "2018-09-05T14:26:03",
            "AllocationStatus": "DO_CREATED"
          }
        },
        "SplitLines": ""
      }
    },
    "DistributionOrders": {
      "DistributionOrder": {
        "DONbr": 12614263030,
        "OrderType": "Customer Order",
        "DOFulfillmentStatus": "Draft",
        "MonetaryValue": 32390,
        "MonetaryValueCurrencyCode": "CLP",
        "MustReleaseByDTTM": "2018-09-06T21:00:00",
        "ReferenceField1": "ATG",
        "ReferenceField2": "55.555.555-5",
        "ReferenceField3": "RUT",
        "LineItems": {
          "LineItem": {
            "DOLineNbr": 1,
            "COLineNbr": 5950315,
            "ItemName": 5950315,
            "DOLineStatus": "Draft",
            "OrderedQty": 1,
            "OrderedQtyUOM": "unit",
            "UnitMonetaryValue": 1480,
            "ShippedQuantity": "",
            "SupplyId": "",
            "SupplyDetailId": "",
            "IsCancelled": false,
            "ItemDescription": "RAYOVAC-@PILA ALCALINA AAA X 2"
          }
        }
      }
    },
    "ShipmentDetails": ""
  }
}
```
</p></details></td></tr>

<tr>
    <td>SO.DADI.ORDER.CREATED</td>
    <td><ul><li>so.order</li><li>db.write</li></ul></td>
    <td><b>body</b><ul>
      <li>Id: Tenant + Seller Center Order Id</li>
<li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
     <li>Order: Seller Center Order Information</li>
    <li>OrderItemIds: Seller Center Order Items Ids</li>
      <li>DadiOrder: Dadi Output reponse</li>
    </ul>
    <b>brokerProperties</b>
    <ul>
    <li>CorrelationId: business [fa|so]</li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
  "Id": "231512862",
  "TenantId": "socl",
  "Order": {
    "OrderId": "1512862",
    "CustomerFirstName": "Test",
    "CustomerLastName": "Test",
    "DeliveryInfo":"STS_1234",
    "DeliveryOption":"ShipToStore",
    "StoreId": "1234",
    "OrderNumber": "206569766",
    "PaymentMethod": "CashOnDelivery_Payment",
    "Remarks": "",
    "DeliveryInfo": "",
    "Price": "5070.00",
    "GiftOption": "0",
    "GiftMessage": "",
    "VoucherCode": "",
    "CreatedAt": "2018-09-03 14:52:48",
    "UpdatedAt": "2018-09-03 14:52:48",
    "AddressUpdatedAt": "2018-09-03 17:52:48",
    "AddressBilling": {
      "FirstName": "Test",
      "LastName": "Test",
      "Phone": "",
      "Phone2": "",
      "Address1": "Santiago 123",
      "Address2": "",
      "Address3": "",
      "Address4": "",
      "Address5": "",
      "CustomerEmail": "",
      "City": "METROPOLITANA",
      "Ward": "",
      "Region": "",
      "PostCode": "0013101",
      "Country": "Chile"
    },
    "AddressShipping": {
      "FirstName": "Test",
      "LastName": "Test",
      "Phone": "",
      "Phone2": "",
      "Address1": "Santiago 123",
      "Address2": "SANTIAGO",
      "Address3": "",
      "Address4": "",
      "Address5": "",
      "CustomerEmail": "",
      "City": "Metropolitana, Santiago",
      "Ward": "",
      "Region": "",
      "PostCode": "0013101",
      "Country": "Chile"
    },
    "NationalRegistrationNumber": "55.555.555-5",
    "ItemsCount": "1",
    "PromisedShippingTime": "2018-09-10 14:00:00",
    "ExtraAttributes": "",
    "Statuses": {
      "Status": "pending"
    },
    "BillingType": "boleta"
  },
  "OrderItems": [
    {
      "OrderItemId": "1226509",
      "ShopId": "2012387",
      "OrderId": "1512862",
      "Name": "Pincel Acuarela",
      "Sku": "24SQI/01",
      "Upc": "123456",
      "Variation": "Talla Única",
      "ShopSku": "PL593OS0IVU9CLACL-5872078",
      "ShippingType": "Dropshipping",
      "ItemPrice": "1480.00",
      "PaidPrice": "1480.00",
      "Currency": "CLP",
      "WalletCredits": "0.00",
      "TaxAmount": "236.30",
      "CodCollectableAmount": "",
      "ShippingAmount": "3590.00",
      "ShippingServiceCost": "3574.09",
      "VoucherAmount": "0",
      "VoucherCode": "",
      "Status": "pending",
      "IsProcessable": "1",
      "ShipmentProvider": "Blue Express",
      "IsDigital": "0",
      "DigitalDeliveryInfo": "",
      "TrackingCode": "",
      "TrackingCodePre": "",
      "Reason": "",
      "ReasonDetail": "",
      "PurchaseOrderId": "",
      "PurchaseOrderNumber": "",
      "PackageId": "",
      "PromisedShippingTime": "2018-09-10 14:00:00",
      "ExtraAttributes": "",
      "ShippingProviderType": "express",
      "CreatedAt": "2018-09-03 14:52:48",
      "UpdatedAt": "2018-09-03 17:52:48",
      "ReturnStatus": ""
    }
  ],
  "DadiOrder": {}
}
```
</p></details></td></tr>

<tr>
    <td>FA.ASL.INVOICE.CREATED</td>
    <td><ul><li> db.write</li></ul></td>
    <td><b>body</b><ul>
     <li> Id: Tenant + Seller Center Order Id</li>
<li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
<li>Order: Seller Center Order Information</li>
<li>OrderItemIds: Seller Center Order Items Ids</li>
      <li>OmsOrder: OMS Output reponse</li>
      <li>AslResponse: ASL output reponse</li>
    </ul>
    <b>brokerProperties</b>
    <ul><li>CorrelationId: business [fa|so]</li></ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
  "Id": "131512862",
  "TenandId": "facl",
  "Order": {
    "OrderId": "1512862",
    "CustomerFirstName": "Test",
    "CustomerLastName": "Test",
    "DeliveryInfo":"STS_1234",
    "DeliveryOption":"ShipToStore",
    "StoreId": "1234",
    "OrderNumber": "206569766",
    "PaymentMethod": "CashOnDelivery_Payment",
    "Remarks": "",
    "DeliveryInfo": "",
    "Price": "5070.00",
    "GiftOption": "0",
    "GiftMessage": "",
    "VoucherCode": "",
    "CreatedAt": "2018-09-03 14:52:48",
    "UpdatedAt": "2018-09-03 14:52:48",
    "AddressUpdatedAt": "2018-09-03 17:52:48",
    "AddressBilling": {
      "FirstName": "Test",
      "LastName": "Test",
      "Phone": "",
      "Phone2": "",
      "Address1": "Conde el Sapo 125 125",
      "Address2": "",
      "Address3": "",
      "Address4": "",
      "Address5": "",
      "CustomerEmail": "",
      "City": "METROPOLITANA",
      "Ward": "",
      "Region": "",
      "PostCode": "0013101",
      "Country": "Chile"
    },
    "AddressShipping": {
      "FirstName": "Test",
      "LastName": "Test",
      "Phone": "",
      "Phone2": "",
      "Address1": "Santiago 123",
      "Address2": "SANTIAGO",
      "Address3": "",
      "Address4": "",
      "Address5": "",
      "CustomerEmail": "",
      "City": "Metropolitana, Santiago",
      "Ward": "",
      "Region": "",
      "PostCode": "0013101",
      "Country": "Chile"
    },
    "NationalRegistrationNumber": "55.555.555-5",
    "ItemsCount": "1",
    "PromisedShippingTime": "2018-09-10 14:00:00",
    "ExtraAttributes": "",
    "Statuses": {
      "Status": "pending"
    },
    "BillingType": "boleta"
  },
  "OrderItems": [
    {
      "OrderItemId": "1226509",
      "ShopId": "2012387",
      "OrderId": "1512862",
      "Name": "Pincel Acuarela",
      "Sku": "24SQI/01",
      "Upc": "123456",
      "Variation": "Talla Única",
      "ShopSku": "PL593OS0IVU9CLACL-5872078",
      "ShippingType": "Dropshipping",
      "ItemPrice": "1480.00",
      "PaidPrice": "1480.00",
      "Currency": "CLP",
      "WalletCredits": "0.00",
      "TaxAmount": "236.30",
      "CodCollectableAmount": "",
      "ShippingAmount": "3590.00",
      "ShippingServiceCost": "3574.09",
      "VoucherAmount": "0",
      "VoucherCode": "",
      "Status": "pending",
      "IsProcessable": "1",
      "ShipmentProvider": "Blue Express",
      "IsDigital": "0",
      "DigitalDeliveryInfo": "",
      "TrackingCode": "",
      "TrackingCodePre": "",
      "Reason": "",
      "ReasonDetail": "",
      "PurchaseOrderId": "",
      "PurchaseOrderNumber": "",
      "PackageId": "",
      "PromisedShippingTime": "2018-09-10 14:00:00",
      "ExtraAttributes": "",
      "ShippingProviderType": "express",
      "CreatedAt": "2018-09-03 14:52:48",
      "UpdatedAt": "2018-09-03 17:52:48",
      "ReturnStatus": ""
    }
  ],
  "OmsOrder": {
    "OrderNumber": 5079056101,
    "OrderCreatedDate": "2018-09-05T14:26:02",
    "OrderCaptureDate": "2018-09-05T17:05:00",
    "ExternalOrderNumber": 1512867,
    "OrderSubtotal": 1480,
    "OrderTotal": 32390,
    "OrderCurrency": "CLP",
    "EnteredBy": "",
    "EnteredLocation": "",
    "EntryType": "",
    "Confirmed": true,
    "MinimizeShipments": false,
    "OrderType": "DTC",
    "OrderStatus": "DO Created",
    "LastUpdatedDTTM": "2018-09-05T14:26:03",
    "CustomerInfo": {
      "CustomerId": "10.760.045-0",
      "CustomerFirstName": "Test",
      "CustomerLastName": "Test",
      "CustomerPhone": "",
      "CustomerEmail": ""
    },
    "PaymentDetails": {
      "PaymentDetail": {
        "ExternalPaymentDetailId": 1,
        "PaymentMethod": "Others",
        "CardType": "",
        "AccountNumber": "",
        "AccountDisplayNumber": "",
        "NameAsOnCard": "",
        "CardExpiryMonth": "",
        "CardExpiryYear": "",
        "ReqAuthorizationAmount": 0,
        "ChargeSequence": 1,
        "ReferenceFields": {
          "ReferenceField1": "",
          "ReferenceField2": "",
          "ReferenceField4": "",
          "ReferenceField5": "",
          "ReferenceField6": "",
          "ReferenceField7": ""
        },
        "BillToDetail": {
          "BillToFirstName": "Test",
          "BillToLastName": "Test",
          "BillToAddressLine1": "Conde el Sapo 125",
          "BillToAddressLine2": "",
          "BillToAddressLine3": "",
          "BillToCity": "SANTIAGO CENTRO",
          "BillToState": 13,
          "BillToPostalCode": 366,
          "BillToCountry": "CL",
          "BillToPhone": "",
          "BillToEmail": ""
        }
      }
    },
    "ChargeDetails": {
      "ChargeDetail": {
        "ExtChargeDetailId": 144009841208,
        "ChargeCategory": "Misc",
        "ChargeName": "Shipping",
        "ChargeAmount": 30910
      }
    },
    "DiscountDetails": "",
    "Notes": "",
    "WMNotes": "",
    "ReferenceFields": {
      "ReferenceField1": "ATG",
      "ReferenceField2": "55.555.555-5",
      "ReferenceField3": "RUT"
    },
    "CustomFieldList": {
      "CustomField": [
        {
          "Name": "ActionType",
          "Value": ""
        },
        {
          "Name": "Email",
          "Value": ""
        },
        {
          "Name": "Error",
          "Value": ""
        },
        {
          "Name": "FirstName",
          "Value": ""
        },
        {
          "Name": "LastName",
          "Value": ""
        },
        {
          "Name": "Phone",
          "Value": ""
        },
        {
          "Name": "RUTID",
          "Value": ""
        },
        {
          "Name": "Relation",
          "Value": ""
        },
        {
          "Name": "TipoDoc",
          "Value": ""
        }
      ]
    },
    "WMProcessInfo": {
      "RefTextField1": 2000,
      "RefTextField2": "",
      "RefTextField3": "",
      "RefTextField4": "",
      "RefTextField5": "",
      "RefTextField6": ""
    },
    "OrderLines": {
      "OrderLine": {
        "LineNumber": 5950315,
        "OrderLineCreatedDate": "2018-09-05T14:26:02",
        "OrderLineStatus": "DO Created",
        "ItemID": 5950315,
        "ItemDescription": "RAYOVAC-@PILA ALCALINA",
        "LineTotal": 1480,
        "LastUpdatedDTTM": "2018-09-05T14:26:02",
        "PriceInfo": {
          "Price": 1480
        },
        "Quantity": {
          "OrderedQty": 1,
          "OrderedQtyUOM": "unit",
          "CancelledQty": 0,
          "TotalAllocatedQty": 1,
          "TotalCancelledQty": 0
        },
        "ShippingInfo": {
          "PromisedDeliveryBy": "2018-09-10T17:00:00",
          "RequestedDeliveryBy": "2018-09-10T17:00:00",
          "DesignatedServiceLevelCode": "AD",
          "ShipToFacility": "",
          "DeliveryOption": "Ship to address",
          "ShippingAddress": {
            "ShipToFirstName": "Test",
            "ShipToLastName": "Test",
            "ShipToAddressLine1": "Conde el Sapo 125",
            "ShipToAddressLine2": "",
            "ShipToAddressLine3": "",
            "ShipToCity": "SANTIAGO CENTRO",
            "ShipToState": 13,
            "ShipToPostalCode": 366,
            "ShipToCounty": "",
            "ShipToCountry": "CL",
            "ShipToPhone": "",
            "ShipToEmail": "",
            "ShipToFax": "",
            "ShipToLatitude": "",
            "ShipToLongitude": "",
            "ShipToVerifiedByAVS": false,
            "ShipToLocationType": ""
          }
        },
        "DiscountDetails": "",
        "ChargeDetails": "",
        "Notes": "",
        "WMNotes": {
          "WMNote": [
            {
              "NoteType": "DDate",
              "NoteCode": "",
              "CommentText": "2018-09-10T17:00:00.000Z"
            },
            {
              "NoteType": "LocldId",
              "NoteCode": "",
              "CommentText": 366
            },
            {
              "NoteType": "Region",
              "NoteCode": "",
              "CommentText": "REGION METROPOLITANA"
            },
            {
              "NoteType": "Comuna",
              "NoteCode": "",
              "CommentText": "SANTIAGO CENTRO"
            },
            {
              "NoteType": "Locality",
              "NoteCode": "",
              "CommentText": "SANTIAGO CENTRO"
            },
            {
              "NoteType": "SAddress",
              "NoteCode": "",
              "CommentText": "Santiago 123"
            },
            {
              "NoteType": "Ndoc",
              "NoteCode": "",
              "CommentText": "10.760.045-0"
            },
            {
              "NoteType": "TipoDoc",
              "NoteCode": "",
              "CommentText": "RUT"
            }
          ]
        },
        "LineReferenceFields": {
          "ReferenceField1": "",
          "ReferenceField2": false,
          "ReferenceField3": "AUTHORIZED",
          "ReferenceField4": "",
          "ReferenceField5": "AD",
          "ReferenceNumber1": "",
          "ReferenceNumber2": 0
        },
        "CustomFieldList": {
          "CustomField": [
            {
              "Name": "RUTID",
              "Value": ""
            },
            {
              "Name": "Relation",
              "Value": ""
            },
            {
              "Name": "Phone",
              "Value": ""
            },
            {
              "Name": "Email",
              "Value": ""
            },
            {
              "Name": "TipoDoc",
              "Value": ""
            },
            {
              "Name": "FirstName",
              "Value": ""
            },
            {
              "Name": "LastName",
              "Value": ""
            },
            {
              "Name": "ItemSubclass",
              "Value": ""
            }
          ]
        },
        "LineWMProcessInfo": {
          "LineRefTextField1": "",
          "LineRefTextField2": "",
          "LineRefTextField3": 144009841208,
          "LineRefTextField4": "",
          "LineRefTextField5": "",
          "LineRefTextField6": ""
        },
        "AllocationDetails": {
          "AllocationDetail": {
            "ItemID": 5950315,
            "AllocatedQuantity": 1,
            "AllocatedQtyUOM": "unit",
            "SupplyType": "OH",
            "SupplyID": "",
            "SupplyDetailID": "",
            "IsVirtualAllocation": false,
            "TierId": "Shipping Anywhere",
            "OriginFacilityAliasID": 2000,
            "FacilityType": "DC",
            "CommittedShipDTTM": "2018-09-09T18:45:00",
            "CommittedDeliveryDTTM": "2018-09-09T20:45:00",
            "MustReleaseByDTTM": "2018-09-06T21:00:00",
            "MustShipByDTTM": "2018-09-09T18:45:00",
            "CreatedDTTM": "2018-09-05T14:26:03",
            "ModifiedDTTM": "2018-09-05T14:26:03",
            "AllocationStatus": "DO_CREATED"
          }
        },
        "SplitLines": ""
      }
    },
    "DistributionOrders": {
      "DistributionOrder": {
        "DONbr": 12614263030,
        "OrderType": "Customer Order",
        "DOFulfillmentStatus": "Draft",
        "MonetaryValue": 32390,
        "MonetaryValueCurrencyCode": "CLP",
        "MustReleaseByDTTM": "2018-09-06T21:00:00",
        "ReferenceField1": "ATG",
        "ReferenceField2": "10.760.045-0",
        "ReferenceField3": "RUT",
        "LineItems": {
          "LineItem": {
            "DOLineNbr": 1,
            "COLineNbr": 5950315,
            "ItemName": 5950315,
            "DOLineStatus": "Draft",
            "OrderedQty": 1,
            "OrderedQtyUOM": "unit",
            "UnitMonetaryValue": 1480,
            "ShippedQuantity": "",
            "SupplyId": "",
            "SupplyDetailId": "",
            "IsCancelled": false,
            "ItemDescription": "RAYOVAC-@PILA ALCALINA AAA X 2"
          }
        }
      }
    },
    "ShipmentDetails": ""
  },
  "AslResponse":{
    "respose":'<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body><ns4:asl-purchase-order-inscription-response xmlns:ns4="http://www.falabella.com/schemas/asl-purchase-order-inscription-response" xmlns:ns3="http://www.falabella.com/schemas/asl-header" xmlns:ns2="http://www.falabella.com/schemas/asl-common" xmlns="http://www.falabella.com/schemas/asl-purchase-order-inscription"><ns4:response code="0">Inscripción realizada en forma exitosa</ns4:response></ns4:asl-purchase-order-inscription-response></soap:Body></soap:Envelope>'
  }
}
```
</p></details></td></tr>

<tr>
    <td>SO.UXPOS.INVOICE.CREATED</td>
    <td><ul><li>db.write</li></ul></td>
    <td><b>body</b><ul>
     <li> Id: Tenant + Seller Center Order Id</li>
<li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
<li>Order: Seller Center Order Information</li>
<li>OrderItemIds: Seller Center Order Items Ids</li>
      <li>DadiOrder: Uxpos output reponse</li>
      <li>UxposResponse: Uxpos output reponse</li>
    </ul>
    <b>brokerProperties</b>
    <ul>
    <li>CorrelationId: business [fa|so]</li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
  "Id": "231512862",
  "TenandId": "socl",
  "Order": {
    "OrderId": "1512862",
    "CustomerFirstName": "Test",
    "CustomerLastName": "Test",
    "DeliveryInfo":"STS_1234",
    "DeliveryOption":"ShipToStore",
    "StoreId": "1234",
    "OrderNumber": "206569766",
    "PaymentMethod": "CashOnDelivery_Payment",
    "Remarks": "",
    "DeliveryInfo": "",
    "Price": "5070.00",
    "GiftOption": "0",
    "GiftMessage": "",
    "VoucherCode": "",
    "CreatedAt": "2018-09-03 14:52:48",
    "UpdatedAt": "2018-09-03 14:52:48",
    "AddressUpdatedAt": "2018-09-03 17:52:48",
    "AddressBilling": {
      "FirstName": "Test",
      "LastName": "Test",
      "Phone": "",
      "Phone2": "",
      "Address1": "Conde el Sapo 125 125",
      "Address2": "",
      "Address3": "",
      "Address4": "",
      "Address5": "",
      "CustomerEmail": "",
      "City": "METROPOLITANA",
      "Ward": "",
      "Region": "",
      "PostCode": "0013101",
      "Country": "Chile"
    },
    "AddressShipping": {
      "FirstName": "Test",
      "LastName": "Test",
      "Phone": "",
      "Phone2": "",
      "Address1": "Santiago 123",
      "Address2": "SANTIAGO",
      "Address3": "",
      "Address4": "",
      "Address5": "",
      "CustomerEmail": "",
      "City": "Metropolitana, Santiago",
      "Ward": "",
      "Region": "",
      "PostCode": "0013101",
      "Country": "Chile"
    },
    "NationalRegistrationNumber": "55.555.555-5",
    "ItemsCount": "1",
    "PromisedShippingTime": "2018-09-10 14:00:00",
    "ExtraAttributes": "",
    "Statuses": {
      "Status": "pending"
    },
    "BillingType": "boleta"
  },
  "OrderItems": [
    {
      "OrderItemId": "1226509",
      "ShopId": "2012387",
      "OrderId": "1512862",
      "Name": "Pincel Acuarela Pelo Sintético, Imitación Ardilla 1",
      "Sku": "24SQI/01",
      "Upc": "123456",
      "Variation": "Talla Única",
      "ShopSku": "PL593OS0IVU9CLACL-5872078",
      "ShippingType": "Dropshipping",
      "ItemPrice": "1480.00",
      "PaidPrice": "1480.00",
      "Currency": "CLP",
      "WalletCredits": "0.00",
      "TaxAmount": "236.30",
      "CodCollectableAmount": "",
      "ShippingAmount": "3590.00",
      "ShippingServiceCost": "3574.09",
      "VoucherAmount": "0",
      "VoucherCode": "",
      "Status": "pending",
      "IsProcessable": "1",
      "ShipmentProvider": "Blue Express",
      "IsDigital": "0",
      "DigitalDeliveryInfo": "",
      "TrackingCode": "",
      "TrackingCodePre": "",
      "Reason": "",
      "ReasonDetail": "",
      "PurchaseOrderId": "",
      "PurchaseOrderNumber": "",
      "PackageId": "",
      "PromisedShippingTime": "2018-09-10 14:00:00",
      "ExtraAttributes": "",
      "ShippingProviderType": "express",
      "CreatedAt": "2018-09-03 14:52:48",
      "UpdatedAt": "2018-09-03 17:52:48",
      "ReturnStatus": ""
    }
  ],
  "DadiOrder": {},
  "UxposResponse":{}
}
```
</p></details></td></tr>

<tr>
    <td>SO.ORDER.STATUS.INVOICED</td>
    <td>
    <ul><li>so.order</li></ul></td>
    <td><b>body</b><ul>
      <li>Id: Tenant + Seller Center Order Id</li>
      <li>OrderId: Seller Center Order Id</li>
      <li>TenantId: Tenant [soar|soco|socl|sope|somx]</li>
      <li>InternalOrderId: internal order id</li>
      <li>OrderNumber: order number</li>
      <li>ItemsId: Seller Center Order Items Ids</li>
      <li>ShipmentProvider</li>
    </ul>
    <b>brokerProperties</b>
    </td><td>
<details>
  <summary>Click</summary>
<p>


```json
{
  "Id": 2312345,
  "OrderId": 12345,
  "TenantId": "socl",
  "InternalOrderId": "5566",
  "ItemsId": [1234,5678],
  "ShipmentProvider" : "Sodimac"
}
```
</p></details></td></tr>

<tr>
    <td>ORDER.READYTOSHIP</td>
    <td><ul>
    <li>db.writer</li>
    <li>linio.order</li>
    </ul></td>
    <td><b>body</b>
    <ul>
      <li>Id: Tenant + Seller Center Order Id </li>
      <li>OrderId: Seller Center Order Id</li>
      <li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
      <li>InternalOrderId: internal order id</li>
      <li>ItemsId: Seller Center Order Items Ids</li>
      <li>ShippingProvider: shipping provider [Falabella|Sodimac]</li>
      <li>Status: order status [ready_to_ship]</li>
    </ul>
    <b>brokerProperties</b>
    <ul>
    <li>CorrelationId: business [fa|so]</li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>


```json
{
  "Id": 1312345,
  "OrderId": 12345,
  "TenantId": "facl",
  "InternalOrderId": "5566",
  "ItemsId": [1234,5678],
  "ShippingProvider": "Falabella",
  "Status": "ready_to_ship"
}
```
</p></details></td></tr>

<tr>
    <td>INVENTORY.UPDATED</td>
    <td><ul>
    <li>linio.inventory</li>
    </ul></td>
    <td><b>body</b>
    <ul>
      <li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
      <li>Products: List of products object
        <ul> 
          <li>sku</li>
          <li>warehouse</li>
          <li>quantity</li>
        </ul>
      </li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>


```json
{
  "TenantId": "facl",
  "Products": [{
    "sku": "123",
    "warehouse": "9000",
    "quantity": 123
  }]
}
```
</p></details></td></tr>

<tr>
    <td>LINIO.PRODUCT.CREATED</td>
    <td><ul>
    <li>linio.product</li>
    </ul></td>
    <td><b>body</b>
    <ul>
      <li>Sku: Product SKU</li>
      <li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
  "Sku": "1312345",
  "TenantId": "facl"
}
```
</p></details></td></tr>
<tr>
    <td>EXEC.PRODUCTS.FETCHED</td>
    <td><ul>
    <li>linio.products</li>
    </ul></td>
    <td><b>body</b>
    <ul>
      <li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
      <li>Page: page to look up in products pagination</li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
   "TenantId": "facl",
   "Page": 1
}

```
</p></details></td></tr>
<tr>
    <td>CMR.PRICE.UPDATED</td>
    <td><ul>
    <li>linio.price</li>
    </ul></td>
    <td><b>body</b>
    <ul>
     <li>skus: Product SKUs</li>
      <li>tenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
   "tenantId":"facl",
   "skus": [
     {
       "sellerSku": "6376016",
       "price": 55.25,
       "validFrom": "2019-01-25T20:32:44+00:00",
       "validTo": "2019-02-25T20:32:44+00:00"
     }
   ]
 }
 ```
</p></details></td></tr>
<tr>
    <td>ORDER.INVOICED</td>
    <td><ul>
    <li>fa.order.url</li>
    <li>linio.order</li>
    <li>so.order.url</li>
    </ul></td>
    <td><b>body</b>
    <ul>
      <li>Id: Tenant + Seller Center Order Id </li>
      <li>OrderNumber: Seller Center Order Id</li>
      <li>BillingType: Billing type [boleta|factura]</li>
      <li>InternalOrderId: internal order id</li>
      <li>TenantId: Tenant [faar|faco|facl|fape]</li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
  "Id": "13123456",
  "OrderNumber": "123456",
  "BillingType": "boleta",
  "InternalOrderId": "5566",
  "TenantId":"facl",
}
 ```
</p></details></td></tr>
<tr>
    <td>INVOICE.URL.UPDATED</td>
    <td><ul>
    <li>linio.order</li>
    </ul></td>
    <td><b>body</b>
    <ul>
      <li>Id: Tenant + Seller Center Order Id </li>
      <li>OrderNumber: Seller Center Order Id</li>
      <li>InvoicedOrderUrl: Invoiced order document url to update</li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
  "Id": "13123456",
  "OrderNumber": "123456",
  "InvoicedOrderUrl": "https://example.com"
}
 ```
</p></details></td></tr>
<tr>
    <td>EXEC.DELIVERY.DATE.FETCHED</td>
    <td><ul>
    <li>fa.delivery</li>
    </ul></td>
    <td><b>body</b>
    <ul>
      <li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
    </ul>
     <b>brokerProperties</b>
    <ul>
    <li>ScheduledEnqueueTimeUtc: DATETIME</li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
   "TenantId": "facl",
}

```
</p></details></td></tr>
<tr>
    <td>EXEC.PRODUCT.UPDATE</td>
    <td><ul>
    <li>linio.product</li>
    </ul></td>
    <td><b>body</b>
    <ul>
      <li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
    </ul>
    <b>brokerProperties</b>
    <ul>
    <li>ScheduledEnqueueTimeUtc: DATETIME</li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
   "TenantId": "facl",
}

```
</p></details></td></tr>
<tr>
    <td>FA.PRICE.EXPIRED</td>
    <td><ul>
    <li>fa.price</li>
    </ul></td>
    <td><b>body</b>
    <ul>
      <li>tenant: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
      <li>sku</li>
    </ul>
    <b>brokerProperties</b>
    <ul>
    <li>ScheduledEnqueueTimeUtc: DATETIME</li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
   "tenant": "facl",
   "sku": "12345489"
}

```
</p></details></td></tr>
<tr>
    <td>LEADTIME.PRODUCT.UPDATED</td>
    <td><ul>
    <li>linio.dts</li>
    </ul></td>
    <td><b>body</b>
    <ul>
      <li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
      <li>Skus</li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
   "TenantId": "facl",
   "Skus": [ {
      "sellerSku": "6376016",
      "dispatchTime": 2
    },
     {
      "sellerSku": "12312sdgsd",
      "dispatchTime": 5
    },
    {
      "sellerSku": "63ge4t344",
      "dispatchTime": 1
    }
]
}

```
</p></details></td></tr>
<tr>
    <td>LINIO.ORDER.STATUS</td>
    <td><ul>
    <li>db.write</li>
    </ul></td>
    <td><b>body</b>
    <ul>
      <li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
      <li>Id</li>
      <li>OrderId: Seller Center Order Id</li>
      <li>OrderItemIds: Seller Center Order Items Ids</li>
      <li>NewStatus : canceled</li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
  "Id":"131469208",
  "TenantId": "facl",
  "OrderId": "1469208",
  "OrderItemIds": ["123", "432"],
  "NewStatus": "canceled"
}

```
</p></details></td></tr>
<tr>
    <td>ORDER.INVOICED</td>
    <td><ul>
    <li>linio.order</li>
    <li>fa.order.url</li>
    </ul></td>
    <td><b>body</b>
    <ul>
      <li>Id</li>
      <li>OrderId: Seller Center Order Id</li>
      <li>OrderNumber: Order number</li>
      <li>BillingType: Order billing type</li>
      <li>TenantId: Tenant [faar|faco|facl|fape|soar|soco|socl|sope|somx]</li>
      <li>InternalOrderId: Internal order id</li>
    </ul>
    </td><td>
<details>
  <summary>Click</summary>
<p>

```json
{
  "Id": "13123456",
  "OrderId": "123456",
  "OrderNumber": "123456",
  "BillingType": "boleta",
  "TenantId": "facl",
  "InternalOrderId": 65432131
}

```
</p></details></td></tr>

</table>

### External Topics

<table style="font-size:12px;">
<tr>
    <th width="10%">TOPIC</th>
    <th width="10%">SUBSCRIPTION</td>
    <th width="10%">SOURCE</td>
    <th width="40%">MESSAGE PROPERTIES</th>
    <th width="30%">EXAMPLE</th>
</tr>
<tr>
    <td>availabilitynotification</td>
    <td><ul>
    <li>thor</li>
    </ul></td>
    <td><b>body</b>
    <ul>
      <li>metadata.Availability.AvailabilityDetails.AvailabilityDetail: List of inventory stock updates
        <ul> 
          <li>SKU</li>
          <li>FacilityId</li>
          <li>ATCQuantity</li>
        </ul>
      </li>
    </ul>
    </td>
    <td>OMS</td>    
    <td>
<details>
  <summary>Click</summary>
<p>


```json
{
    "eventId": "05a1c531-6733-4b98-8410-9dbb3ea416f6",
    "eventType": "inventoryAvailabilityEvent",
    "entityId": "508f200e814c19736de862be",
    "entityType": "AvailabilityNotification",
    "timestamp": "1526395872",
    "datetime": "2018-05-14T14:33:04.000Z",
    "version": "1.0",
    "country": "CL",
    "commerce": "Falabella",
    "channel": "OMS",
    "mimeType": "application/json",
    "metadata": {
        "Availability": {
            "TransactionNumber": "TransactionNumber0",
            "TransactionType": "StartSync",
            "TransactionDateTime": "2006-05-04T18:13:51",
            "ViewName": "THOR_XXXXXXX",
            "ViewConfiguration": "ViewConfiguration0",
            "SyncInput": 0,
            "SyncCount": 0,
            "AvailabilityDetails": {
                "AvailabilityDetail": [
                    {
                        "BusinessUnit": "BusinessU",
                        "FacilityId": "9000",
                        "SKU": "1234567890",
                        "ATCQuantity": 5,
                        "ATCStatus": "In Stock"
                    },
                    {
                        "BusinessUnit": "BusinessU",
                        "FacilityId": "9000",
                        "SKU": "1234567891",
                        "ATCQuantity": 1,
                        "ATCStatus": "In Stock"
                    }
                ]
            }
        }
    }
}

```
</p></details></td></tr>
<tr>
    <td>price_events</td>
    <td><ul>
    <li>thor</li>
    </ul></td>
    <td><b>body</b>
    <ul>
      <li>data: Array of update price events</li>
      <li>country</li>
    </ul>
    </td>
    <td>ATG</td>    
    <td>
<details>
  <summary>Click</summary>
<p>

```json
{  
   "eventId":"05a1c531-6733-4b98-8410-9dbb3ea416f6",
   "eventType":"priceUpdate",
   "entityType":"price",
   "timestamp":null,
   "datetime":"2014-06-25T00:00:00.000Z",
   "version":1.1,
   "country":"CL",
   "commerce":"Falabella",
   "channel":"WEB",
   "mimeType":"application/json",
   "metadata":{  
      "type":"price",
      "priceType":"priceType"
   },
   "data":[  
      {  
         "id":"tablePrimaryKeyId",
         "attributes":{  
            "skuId":"8663875428",
            "originPublishTime":"2014-06-25T00:00:00.000Z",
            "price":{  
               "value":"59.990",
               "currencyCode":"$",
               "validFrom":"2014-06-25T00:00:00.000Z",
               "validUntil":"2019-06-25T00:00:00.000Z",
               "type":"CMR|Normal|Internet|Event|Employee|Margin|Store"    
            }
         }
      }
   ]
}
```
</p></details></td></tr>
</table>
