---
id: documentation index
title: Thor Documentation
sidebar_label: Index
---
# Linio Events Processor [![pipeline status](https://fala.cl/falabella/thor/serverless/badges/master/pipeline.svg)](https://fala.cl/falabella/thor/serverless/commits/master) [![coverage report](https://fala.cl/falabella/thor/serverless/badges/master/coverage.svg)](https://fala.cl/falabella/thor/serverless/commits/master)

Thor is the central hub and broker, responsible of orchestrating event flows across decoupled services to finally create orders in back-office systems.  

Thor exposes a single HTTP endpoint as entrypoint as well as Pub/Sub functionality into a single event-driven experience to process orders.  

## Index
  - [Azure Resources](azure-resources)
  - [Step by Step Guide](step-by-step-guide)
    - [Prerequisites](step-by-step-guide#prerequisites)
    - [Installation](step-by-step-guide#installation)
  - [Development](step-by-step-guide#development)
    - [Login on Azure](step-by-step-guide#login-on-azure)
    - [Creating new functions](step-by-step-guide#creating-new-functions)
    - [Local server](step-by-step-guide#local-server)
    - [Calling back-office systems](step-by-step-guide#calling-back-office-systems)
  - [Scripts](scripts)
  - [Schedulers](#Schedulers)
  - [Go Live Checklist](#go-live-checklist)
  - [Deploy Checklist](#deploy-checklist)
  - [Message Bus](#message-bus)
    - [Topics](#topics)
    - [External Topics](#external-topics)
  - [Linio Seller Center](#linio-seller-center)
  - [Linio API - FAPI](#linio-api)
  - [Thor API](#thor-api)
    - [Webhook Order Created](#webhook-order-created)
    - [Webhook Order Canceled](#webhook-order-canceled)
    - [Webhook Product Created](#webhook-product-created)
    - [API Webtracking status](#api-webtracking-status)
    - [API Refund Product](#api-refund-product)
  - [Architecture](#architecture)
  - [Troubleshooting Guide](#troubleshooting-guide)
  - [Sequence Diagrams](#sequence-diagrams)
  - [Dashboards Falabella](#dashboards-falabella)
  - [Dashboards Sodimac](#dashboards-sodimac)