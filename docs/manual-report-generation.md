---
id: manual report generation
title:  Manual report generation
sidebar_label: Manual report generation
---
## Troubleshooting - Manual report generation

The script is used to generate the manual report for Orders.

---

>``` npm run orders:report <startDate> <EndDate> //DATE_FORMAT: YYYY-MM-DD ```

<b>check `readme.md` for more details</b> - https://fala.cl/adessa/thor/serverless/tree/master#scripts

---

## Output
---

> Files are generated in the root directory with format `${businessName}-data.csv`

---

### Errors
---

| Error | Debug |
|-------|-------------|
| Error requesting orders | Check Seller Center API call Params and response

Check the terminal output and logs for other errors.
