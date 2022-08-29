---
layout: default
title: Integration
nav_order: 2
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
## Using playground
You can explore full api in dashboard api playground section.

To created order execute this graphql query
```graphql
mutation CreateOrder($data:OrdersServiceOrderCreateObject!) {
    createOrder(data: $data)
}
```
Variables

```json
{
    "data": {
        "orderId": "123",
        "barcode": null,
        "shortId": "1wqw2",
        "isFrozen": false,
        "ageLimitation": "N20", // Posable values N18 | N20 
        "pickup": {
            // If address is known value you can use reference id 
                // "addressId": "XXXXXX",
            "address": { 
                "address": "Ozo g. 25, Vilnius, 7150", 
                "contactName": "Your pickup address contact name", 
                "contactPhone": "+370XXXXXXXX", 
                "coordinates": [25.260445,54.708843],
                "notes": "",
                "info": {
                    "postcode": "7150"
                },
            }
        },
        "dropOff": {
            // If address is known value you can use reference id 
            // "addressId": "XXXXXX",
            "address": { 
                // Address is not mandatory
                "coordinates": [25.2503825699727,54.69921435],
                "contactName": "Your drop off address address contact name", 
                "contactPhone": "+370XXXXXXXX", 
                "notes": "Durų kodas 5",
                "info": {
                    "flat": "53", 
                    "floor": "12", 
                    "doorCode": "53#1344", 
                    "postcode": "7100"
                },
            }
        }
    }
}
```

If you specified you contact name and phone in drop section you will receive SMS with tracking link.

```text
Jūsų užsakymas jau pakeliui. Ji galite sekti čia https://st-tracking-barboraexpres.app/xxxx
```

You can also use **REST ENDPOINT** 

```rest
POST https://ha.barbora-go.co/api/rest/order
Content-Type: application/json
Authorization: XXXX

{
    "data": {
        "orderId": "123",
        "barcode": null,
        "shortId": "1wqw2",
        "isFrozen": false,
        "ageLimitation": "N20",
        "pickup": {
            "address": { 
                "address": "Ozo g. 25, Vilnius, 7150", 
                "contactName": "Your pickup address contact name", 
                "contactPhone": "+370XXXXXXXX", 
                "coordinates": [25.260445,54.708843],
                "notes": "",
                "info": {
                    "postcode": "7150"
                },
            }
        },
        "dropOff": {
            "address": { 
                "coordinates": [25.2503825699727,54.69921435],
                "contactName": "Your drop off address address contact name", 
                "contactPhone": "+370XXXXXXXX", 
                "notes": "Durų kodas 5",
                "info": {
                    "flat": "53", 
                    "floor": "12", 
                    "doorCode": "53#1344", 
                    "postcode": "7100"
                },
            }
        }
    }
}
```


## Useful links

1. [GraphQL languages support](https://graphql.org/code)
1. [GraphQL code generator](https://www.graphql-code-generator.com/)