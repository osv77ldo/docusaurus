---
id: schedulers
title: Schedulers
sidebar_label: Schedulers
---
## Schedulers

> <b>Delete Old files from Blob-Storage related to inventory.</b>
___

| Function Name | Blob Name | Runs At | Target Files |
| -------- | -------- | -------- | -------- |
| ScheduleDeleteFilesInContainer     | fa-inventory     | Everyday `12:00 AM`     | Older then 7 days     |
| ScheduleDeleteFilesInContainer     | so-inventory     | Everyday `12:00 AM`     | Older then 3 days     |
| ScheduleDeleteFilesInContainer     | so-prices    | Everyday `12:00 AM`     | Older then 7 days     |
| ScheduleDeleteFilesInContainer     | fa-orders-reports     | Every Sunday `12:00 AM`  | Older then 7 days     |
| ScheduleDeleteFilesInContainer     | so-orders-reports     | Every Sunday  `12:00 AM`   | Older then 7 days     |

<br>

> <b>Fetch Products from SC and Sync with Redis.</b>
___

| Function Name | Runs At |
| -------- | -------- | 
| ScheduleFetchProducts     | Every Day at `08:00 AM`  |

<br>

> <b>Fetch Statistics from SC about Products.</b>
___

| Function Name | Runs At |
| -------- | -------- | 
| ScheduleFetchStatistics     | Every Day at `12:00 PM`  |

<br>

> <b>Fetch API Feed list for Failed and Errored calls from SC and post to Slack Channel.</b>
___
| Function Name | Runs At |
| -------- | -------- | 
| ScheduleGetFeedlist     | Every Day at `03:00 PM`  |

<br>

> <b>Scheduler for ready to ship pending invoiced orders Falabella.</b>
___
| Function Name | Runs At |
| -------- | -------- | 
| ScheduleGetInvoicedOrderFa    | Every day at `04:00 AM`  |

<br>

> <b>Scheduler for ready to ship pending invoiced orders Sodimac.</b>
___
| Function Name | Runs At |
| -------- | -------- | 
| ScheduleGetInvoicedOrderSo   | Every `05` minutes  |

<br>

> <b>Scheduler for uploading daily order summary to blob `fa-orders-reports` | `so-orders-reports`.</b>
___
| Function Name | Runs At |
| -------- | -------- | 
| ScheduleOrdersReportGeneration   | Every Day at `01:00 PM`  |

<br>

> <b>Scheduler for Reporting all Pending orders [SO] [FA].</b>
___
| Function Name | Runs At |
| -------- | -------- | 
| SchedulePendingOrders    | Every Day at `01:00 PM` |

<br>

> <b>Scheduler is used to sync products data in redis from SC [SO] [FA].</b>
___
| Function Name | Runs At |
| -------- | -------- | 
| ScheduleUpdateProduct     | Every `02` minutes  |

> <b>Scheduler is used to send daily order reports email via sendgrid [SO] [FA].</b>
___
| Function Name | Runs At |
| -------- | -------- | 
| ScheduleSendReportMail     | Every Day at `09:30 AM`  |

> <b>Scheduler is used to send daily OMS Inventory File Status [FA].</b>
___
| Function Name | Runs At |
| -------- | -------- | 
| ScheduleAlertOMSInventory     | Every Day at `16:00 PM`  |

