---
layout: default
title: Integration
nav_order: 2
has_children: true
permalink: //integration
---

# Creating your first order

## Basics
You can create your first order using api [playground]()

I highly recommend to read tooling sections. For your stack
1. [NodeJS]()
2. [C#]()
3. [Go]()
4. [Java]()


## Prerequisites

* You have access token.
* Your account is approved by BarboraExpress Team


## Environments

| ENV      | URL |
| ----------- | ----------- |
| PRODUCTION      | https://ha.barboraexpress.com/v1/graphql       |
| TESTING   | https://ha.barbora-go.co/v1/graphql        |

To reach web sockets use `wss` instead of `https`

## Headers

| Header      | Value |
| ----------- | ----------- |
| Authorization      | (Bearer / Token) xxxxx      |
| Organization   | Your organization slug        |

To reach web sockets use `wss` instead of `https`

## Executing basic request
```bash
curl -POST https://ha.barbora-go.co/v1/graphql -h authorization Token XXX
```

```graphql

```
