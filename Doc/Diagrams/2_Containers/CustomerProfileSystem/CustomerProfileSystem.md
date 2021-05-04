Customer Profile System

```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml

Person_Ext(customer, "Customer", "A customer of the service with a subscription")
System(reporting, "Reporting","Requests data from other systems to produce reports")
System(billing, "Billing", "Maintains contract and billing data and initiates payments periodically")
System(survey, "Survey", "Maintains the customer surveys and keeps track of their progress")
System(ticketManagement, "Ticket Manager", "Handles the problem ticket lifecycle")
System_Boundary(customerProfile,"Customer Profile"){
    Container(customerManager, "Customer Maintenance Service", "", "Manages customer data")
    ContainerDb(centralDb, "Central Database", "", "Persists all customer, sysops user, survey, contact and billing data")
    Container(userApp, "Single-Page Application", "", "Provides the frontend to the customer to manage his subscription data")
}

Rel_D(customer, userApp, "Uses")
Rel_D(userApp, customerManager, "Calls")
Rel_R(customerManager, centralDb, "Accesses")
Rel_U(reporting, customerManager, "Makes API call to request data")
Rel_U(billing, customerManager, "Makes API call to request data")
Rel_L(customerManager, ticketManagement, "Requests customer ticket info")
Rel_U(survey, customerManager, "Makes API call to request data")

SHOW_LEGEND(false)
@enduml

```