---
id: scripts
title: Scripts
sidebar_label: Scripts
---

**Send Message to Topic**

_Set "isEncrypted"= false in local.settings.json and pull environment variables again._ More details [here](https://fala.cl/adessa/thor/serverless/wikis/How-test-on-local-env)

```shell
$ npm run push:msg {topicName} {json filepath} {business}
```
**Populate locations collection in database**

_Please be sure that your maps are correctly placed in `./scripts/locations/maps/`._ Run the following command to import maps data in database:
```shell
$ npm run generate:locations
```
**Fetch Variables from Azure**

_Only for Dev environment. Remember to set "isEncrypted" = false in local.settings.json and pull environment variables again._ 

```shell
$ npm run pull:env
```
**Push Order to RTS**

_This requires to manually add 3 enviroment variables: REQUEUE\_COSMOSDB\_KEY, REQUEUE\_COSMOSDB\_ENDPOINT & REQUEUE\_ServiceBusSend_ 

```shell
$ npm run push:rts {id}
```
**Order status report**

_This requires to manually add 2 enviroment variables: REQUEUE\_COSMOSDB\_KEY, REQUEUE\_COSMOSDB\_ENDPOINT_ 

Default statuses are `pending` `allocated` `invoiced > 2hs` and `failed`

Example: npm run order:status all all
Example: npm run order:status facl all
Example: npm run order:status all invoiced
Example: npm run order:status socl failed

```shell
$ npm run order:status {tenant|all} {status|all}
```
**Requeue failed order**

_This requires to manually add 3 enviroment variables: REQUEUE\_COSMOSDB\_KEY, REQUEUE\_COSMOSDB\_ENDPOINT, REQUEUE\_WEBHOOK\_URL_

REQUEUE_WEBHOOK_URL must be just the base url, ie: `http://localhost:7071/`

Example: npm run requeue:order 13645372 facl q8eyr7wjskfkfi==

```shell
$ npm run requeue:order {tenantId} {token} {id}
```
> Parameter `id` in the above command should be Array i.e [id1,id2,id3]

> After script execution the files `requeueReport.json` and `requeueLogs.json` are created on your local System in `output` folder - Path `scripts/requeueOrder/output`.

> The `requeueReport.json` contains the final status of all order after requeuing.

> The `requeueLogs.json` contains the logs related to order for debugging and reinjecting again in case of any error.

> <b>Please Note</b> : the previous data in the files are overwritten on each script run. so make sure to copy previous logs and report ,if needed.

> The script checks the order status for `1 min` in case it is not invoiced. you can change the `maxRetryCount` in script if needed.

**Generate orders report datewise**

_This requires to manually add 4 enviroment variables: COSMOSDB\_KEY, COSMOSDB\_ENDPOINT, SELLER\CENTER\_BASE\_URLS,SELLER\_CENTER\_CREDENTIALs_

Example: npm run orders:report  2019-07-21 2019-07-22

```shell
$ npm run orders:report <startDate> <EndDate> //DATE_FORMAT: YYYY-MM-DD
```

**Generate orders on Linio Staging**

_IMPORTANT: This requires to manually create an account on linio webpage, add an address, credit card payment data & a 'dirección de factura'_

_Also requires to run `npm install puppeteer` on console to install all necessary files to run this_

Example: npm run generate:orders scripts/puppeteer/configs/config.pe.json

```shell
$ npm run generate:orders {config-json-path} (Run-on-Chrome: true)
```

config.json example

```json
{
  "country": "pe",
  "email": "federico.casares@wolox.com.ar",
  "password": "123456",
  "card_cvv": "123",
  "cash": true,
  "orders": [
    { "products": ["SW570FA72DWTPEAMZ"], "factura": false },
    { "products": ["SW570FA66DWZPEAMZ"], "factura": true },
    { "products": ["SW570FA64DXBPEAMZ"], "factura": true },
    { "products": ["SW570FA72DWTPEAMZ", "SW570FA64DXBPEAMZ", "SW570FA66DWZPEAMZ"], "factura": false }
  ]
}
```
