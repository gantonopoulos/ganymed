# Title
knowledgeBase System Architecture with separate Database

## Status
Approved

## Context
knowledgeBase's Database is largely independent from any other system activity. 
Since it contains invaluable information and it will incrementally grow in size and we would like to be able to 
keep it separately from the rest of the system, be able to deploy it and replicate it independently, to protect
it against data loss.

## Decision
The knowledgeBase's Database will be separated from the main Database and placed under the knowledgeBase service as independent.

## Consequences
Additional Database administration effort and cost (e.g. licensing etc).