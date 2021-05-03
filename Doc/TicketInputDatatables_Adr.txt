# Title
Ticket Input Data Tables structure

## Status
Approved

## Context
The micro-services need a to maintain and present to the user only the data need to create a new ticket.
This will ensure a lean micro-service.

## Decision
We have identified as such the Customer-Table's data and the Contract-Table's.
The data of the new ticket will be transmitted to the Load-Balancer (and subsequently to the ticket system) 
in a special format.

## Consequences
Synchronization effort with the central Database.