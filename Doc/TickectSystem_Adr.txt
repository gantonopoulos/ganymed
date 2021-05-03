# Title
General Ticket System Architecture

## Status
Approved

## Context
We need an elastic system, that can respond to Customer access spikes. 
We need a highly testable system to ensure robustness and quick response to change.

## Decision
We decided to implement the Ticket System using a Micro-service Architecture. This architecture offers high elasticity and fault tolerance and
we will be able to implement changes to the system at a high rate thanks to its high testability. 
Ticketing need not be highly performing but rather reliable, so we can get away with the performance issues of a Micro-service architecture.
Finally we already have a good CI/CD infrastructure which we can leverage to support this transition.

## Consequences
We sacrifice performance and have to deal with balancing the simultaneous ticket requests to our ticket system.
To that end we have to put extra effort to develop a load balancer.