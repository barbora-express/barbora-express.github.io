---
layout: default
title: Integration
nav_order: 2
has_children: true
permalink: //integration
---

# Creating your first order
## Prerequisites

* You have access token.
* Your account is approved by BarboraExpress Team

## Environments

| ENV      | URL | Dashboard | Tracking Page | 
| ----------- | ----------- | --- | --- |
| PRODUCTION      | https://ha.barboraexpress.com/v1/graphql | https://dashboard.barboraexpress.lt | https://tracking.barboraexpress.lt
| TESTING   | https://ha.barbora-go.co/v1/graphql        | https://st-dashboard-barboraexpress.app | https://st-tracking-barboraexpres.app

To reach web sockets use `wss` instead of `https`

Use same user logins for production and testing environments. Keep in mind if you first time logging in to testing environment it will prompt you to create new organization.

Organizations in testing and production are separate entities.

> Only login credentials are shared across multiple environments

## Headers

| Header      | Value |
| ----------- | ----------- |
| Authorization      | (Bearer / Token) xxxxx      |
| Organization   | Your organization slug        |

To reach web sockets use `wss` instead of `https`

## Executing basic request
```bash
curl -POST https://ha.barbora-go.co/v1/graphql -h authorization  Token XXX
```

## Using playground
You can explore full api in dashboard api playground section.

To created order execute this graphql query
```graphql
mutation CreateOrder($data: OrderCreateObject!) {
    id
}
```
Variables
```json
{
    "data": {
        "orderId": "XXX", // Have to be unique in your organization.
        "xzc"
    }
}
```

If you specified you contact name and phone in drop section you will receive SMS with tracking link.

```text
Jūsų užsakymas jau pakeliui. Ji galite sekti čia https://st-tracking-barboraexpres.app/xxxx

```
