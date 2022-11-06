---
layout: default
title: Introduction
nav_order: 0
permalink: //
---
# Introduction

Barbora Express API is intended for use by merchants who want to use Barbora Express as a last mile carrier partner for their deliveries.
For more info, get in touch: kristupas.pajeda@barboraexpress.lt

### Order creation process

Order can be created via Self Service dashboard or API.

TODO: implement OrderCreate restrictions !!! (same as in SS)
#Submitting order when there is no capacity will lead to `NoCapacityError` this indicates that currently we don't have available couriers.
#Example submitting order at 04:00AM

### Order lifecyle

![Workflow](./assets/workflow.drawio.svg)


1. Order created using self service dashboard or API
1. Order will go to planned state. At this point we know ETA
**There is two types of ETA.**
    1.`INITIAL` - Calculated on first planned occurrence. After this point `INITIAL` ETA will not be changed.
    2. `CURRENT` - Calculated approximately every 1 minute. 

1. When order status changes to `ACTIVE` this indicates this indicates that order is proposed to courier. Courier can decline offer, if offer is declined order will move to `NEED_COURIER` status
1. If courier accepts offer status will change to `WAITING_FOR_COURIER` this indicates that courier is arriving to pickup location. Status can change if courier disappear, in case of this status will change to `NEED_COURIER`
1. Courier will arrive to picking center. After successfully collecting orders status will change to `IN_TRANSIT` if for some reason he will not be able to collect package. Package status will change to `NEED_COURIER` (Example package is not ready to pickup)
1. After successfully collecting all packages. Courier starts delivering. `STARTED` status indicates that courier is going to delivery location.
1. If for some reason courier is not present, (AKA we don't get information from courier for at least 30min) order status will change to `COURIER_MISSING`. This indicates that courier is not present but he have order in his possession.
1. After the order was given to the customer, courier have to complete the order in the app changing the status of the order to `COMPLETED`
1. At any given point courier can fail order. (Car accident, Customer not found) Each case are handled by customer support individually. Courier has to go through a process in the app indicating why fail occurred and after the process is complete the status changes to `FAILED`.

### Order tracking

At any given point customer can track current order status and location.
Customer will receive SMS message when order status reaches `PLANNED` status.

### Webhooks

On every status change webhook will be set to merchant api endpoint. This allows merchant systems to track progress in internal systems.

### Order delivery pricing

Order price is calculated on order creation, and will be finalized on terminal state `COMPLETED` | `FAILED`
