---
id: go live checklist
title: Go Live checklist
sidebar_label: Go live Checklist
---

1. Configure Seller Center Credentials on terraform environment variables Secrets 
2. Configure URLs for back offices systems on Terraform variables
3. Enable/Disable feature flags on terraform environment variables Secrets
    - `ENABLE_FUNCTION_SCHEDULE_FETCH_PRODUCT`
    - `ENABLE_FUNCTION_SCHEDULE_GET_FEED_LIST`
    - `ENABLE_FUNCTION_SCHEDULE_GET_STATISTICS`
    - `ENABLE_FUNCTION_SCHEDULE_UPDATE_PRODUCT`
4. Execute `npm run generate:locations` to populate locations on database
5. Setup Webhooks on Seller Center ([See Webhooks](#thor-api))

### Deploy Checklist

1. Check all new variables exists and have correct data stored and deployed.
1. Run Serverless CI pipeline and deploy in the next 10 minutes.
1. Once deployed check all `tenant:UpdateProductsTaskRunning` keys in redis are in `0`