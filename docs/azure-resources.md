---
id: azure resources
title: Azure Resources
sidebar_label: Azure Resources
---

## Azure Resources

The functions are deployed in the [ecommerce-linio-thor](https://portal.azure.com/#@falabella.onmicrosoft.com/resource/subscriptions/33e42778-48ed-42b6-a61d-dbb6a9454719/resourceGroups/ecommerce-linio-thor/overview) resource group.

**Main Resources List:**

| Name | Type | Description | Environment |
|------|------|-------------|-------------|
| [ThorFunctionsDev](https://portal.azure.com/#blade/WebsitesExtension/FunctionsIFrameBlade/id/%2Fsubscriptions%2F33e42778-48ed-42b6-a61d-dbb6a9454719%2FresourceGroups%2Fecommerce-linio-thor%2Fproviders%2FMicrosoft.Web%2Fsites%2FThorFunctionsDev) | Functions App | Container for the Azure functions. | Dev |
| [ThorFunctionsTest](https://portal.azure.com/#blade/WebsitesExtension/FunctionsIFrameBlade/id/%2Fsubscriptions%2F33e42778-48ed-42b6-a61d-dbb6a9454719%2FresourceGroups%2Fecommerce-linio-thor%2Fproviders%2FMicrosoft.Web%2Fsites%2FThorFunctionsTest) | Functions App | Container for the Azure functions. Functions are deployed here. | Test |
| [ThorFunctionsProd](https://portal.azure.com/#blade/WebsitesExtension/FunctionsIFrameBlade/id/%2Fsubscriptions%2F33e42778-48ed-42b6-a61d-dbb6a9454719%2FresourceGroups%2Fecommerce-linio-thor%2Fproviders%2FMicrosoft.Web%2Fsites%2FThorFunctionsProd) | Functions App | Container for the Azure functions. Functions are deployed here. | Prod |
| [ThorServicePlan](https://portal.azure.com/#@falabella.onmicrosoft.com/resource/subscriptions/33e42778-48ed-42b6-a61d-dbb6a9454719/resourceGroups/ecommerce-linio-thor/overview) | App Service Plan | Defines the computing resources tier for the Azure Functions | N/A |
| [thorbusdev](https://portal.azure.com/#@falabella.onmicrosoft.com/resource/subscriptions/33e42778-48ed-42b6-a61d-dbb6a9454719/resourceGroups/ecommerce-linio-thor/providers/Microsoft.ServiceBus/namespaces/thorbusdev/overview) | Service Bus | Kafka-like messaging bus | Dev |
| [thorbustest](https://portal.azure.com/#@falabella.onmicrosoft.com/resource/subscriptions/33e42778-48ed-42b6-a61d-dbb6a9454719/resourceGroups/ecommerce-linio-thor/providers/Microsoft.ServiceBus/namespaces/thorbustest/overview) | Service Bus | Kafka-like messaging bus | Test |
| [thorbusprod](https://portal.azure.com/#@falabella.onmicrosoft.com/resource/subscriptions/33e42778-48ed-42b6-a61d-dbb6a9454719/resourceGroups/ecommerce-linio-thor/providers/Microsoft.ServiceBus/namespaces/thorbusprod/overview) | Service Bus | Kafka-like messaging bus | Prod |
| [thor-db-dev](https://portal.azure.com/#@falabella.onmicrosoft.com/resource/subscriptions/33e42778-48ed-42b6-a61d-dbb6a9454719/resourceGroups/ecommerce-linio-thor/providers/Microsoft.DocumentDB/databaseAccounts/thor-db-dev/overview) | Database | CosmosDb | Dev |
| [thor-db-test](https://portal.azure.com/#@falabella.onmicrosoft.com/resource/subscriptions/33e42778-48ed-42b6-a61d-dbb6a9454719/resourceGroups/ecommerce-linio-thor/providers/Microsoft.DocumentDB/databaseAccounts/thor-db-test/overview) | Database | CosmosDb | Test |
| [thor-db-prod](https://portal.azure.com/#@falabella.onmicrosoft.com/resource/subscriptions/33e42778-48ed-42b6-a61d-dbb6a9454719/resourceGroups/ecommerce-linio-thor/providers/Microsoft.DocumentDB/databaseAccounts/thor-db-prod/overview) | Database | CosmosDb | Prod |

Other resources in use:

- Redis Cache
- Blob Storage
