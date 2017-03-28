---
title: Load Testing Chatty I/O
description: 

author: dragon119
manager: christb

pnp.series.title: Optimize Performance
---
# Load Testing Chatty I/O
[!INCLUDE [header](../../_includes/header.md)]

This document summarizes the configuration we used to perform load testing for the Chatt yIO antipattern. You should also read about our [general approach][general approach] to deployment and load testing.

## Deployment

 Option             | Value  
------------------- | -------------
Compute             | Web App
Tier                | P1
Instance Count      | 1
SQL Tier            | P3
Max Pool Size       | 1000

## Test Configuration

The load test project included two web tests, each invoking an HTTP `GET` operation.

The URLs used were:

- http://yourwebapp.azurewebsites.net/chattyproduct/products/{SubcategoryId}
- http://yourwebapp.azurewebsites.net/chunkyproduct/products/{SubcategoryId}

Replace *yourwebapp* with the name of your web application, and
replace *{SubcategoryId}* with subcategory number in the range 1 to 5 generated using the *Generate Random Integer* plugin.

The project also included two load tests, one for each web test. Both load tests were
run against a single deployment but at different times, using the following parameters:

Parameter           | Value
------------------- | ------------:
Initial User Count  | 1
Maximum User Count  | 1000
Step Duration       | 60s
Step Ramp Time      | 0s
Step User Count     | 100
Test Duration       | 15 minutes
Test Warm Up        | 30 seconds

The load test for the http://yourwebapp.azurewebsites.net/chattyproduct/products/{SubcategoryId} web test generated the following results:

![Load-test results][ChattyIO]

The load test for the http://yourwebapp.azurewebsites.net/chunkyproduct/products/{SubcategoryId} web test generated the following results:

![Load-test results][ChunkyIO]

[general approach]: ../load-testing.md

[ChattyIO]: _images/ChattyIO.jpg
[ChunkyIO]: _images/ChunkyIO.jpg