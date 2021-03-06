# Title
Overall system Architecture

## Status
Approved

## Context
We need an architecture solution to tackle the elasticity, lack of extensibility, availability problems of the previous 
monolithic system.

## Decision
We propose a hybrid architecture, of a micro-service approach on the ticket creation and a service-based, with on occasion
independent Databases, for the rest of the system.

## Consequences
Using micro-services we can achieve higher elasticity, and a service-based architecture will provide us with the decoupling 
needed for performing changes easier and achieve high testability and system stability.