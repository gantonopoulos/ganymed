Notification ForwardingSystem

```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml


Person_Ext(customer, "Customer", "A customer of the service with a subscription")
Person(sysopsExpert,"Expert", "Qualified personnel carrying out repairs on the customer site")
System(ticketManagement, "Ticket Manager", "Handles the problem ticket lifecycle")
System(survey, "Survey", "Maintains the customer surveys and keeps track of their progress")

System_Boundary(notificationForwarding,"Notification Forwarding"){
    Container(notificationService, "Notification Service", "", "Notifies customers and experts via e-mail or sms on specific events")        
}

Rel_U(notificationService, sysopsExpert,"Sends SMS")
Rel_U(notificationService, customer,"Sends SMS or E-mail")
Rel_U(survey, notificationService, "Requests pending survey notification to customer")
Rel_L(ticketManagement, notificationService, "Sends expert assignment notifications")

SHOW_LEGEND(false)
@enduml

```