Survey System

```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml

Person_Ext(customer, "Customer", "A customer of the service with a subscription")

System(ticketManagement, "Ticket Manager", "Handles the problem ticket lifecycle")
System(notificationForwarding, "Notification Forwarding", "Notifies customers and experts via e-mail or sms on specific events")
System(customerProfile,"Customer Profile", "Maintains the customer data and activities")
System(reporting, "Reporting","Requests data from other systems to produce reports")

System_Boundary(surveySystem,"Survey"){
    Container(surveyManager, "Survey Service", "", "Manages the survey notification delivery and survey submission")
    ContainerDb(centralDb, "Central Database", "", "Persists all customer, sysops user, survey, contact and billing data")
    Container(userApp, "Single-Page Application", "", "Provides the frontend to the customer to submit a survey")
}

Rel_D(customer, userApp, "Uses")
Rel_D(userApp, surveyManager, "Calls")
Rel_L(surveyManager, centralDb, "Accesses")
Rel_D(surveyManager, customerProfile, "Gets customer data")
Rel_U(reporting, surveyManager, "Gets data")
Rel_D(surveyManager, ticketManagement, "Request ticket completion state")
Rel_R(surveyManager, notificationForwarding, "Requests pending survey notification to customer")
Rel_U(notificationForwarding, customer, "Sends E-Mail")

SHOW_LEGEND(false)
@enduml

```