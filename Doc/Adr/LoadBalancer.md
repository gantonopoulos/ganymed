# Title
Load Balancer System Architecture

## Status
Approved

## Context
On peak hours our Micro-services will be transmitting to the ticket system a large volume of ticket requests.
To avoid loss of information, we need a system which will normalize the load.

## Decision
We introduce a load balancer system, a FIFO Queue whose purpose is ensure a uniform ticket transmission to the ticket system.
This way we minimize the probability that a ticket will be lost due to DOS from the ticket system.

## Consequences
In peak hours there can be a delay between creation and persistence in the ticket system.