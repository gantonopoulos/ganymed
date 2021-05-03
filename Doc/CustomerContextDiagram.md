```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml


Person_Ext(customer, "Customer", "A customer of the service with a subscription")

System(ticketInput, "Ticket Input", "Handles the ticket creation from the customer")
System(customerProfile,"Customer Profile", "Maintains the customer data and activities")
System(survey, "Survey", "Maintains the customer surveys and keeps track of their progress")
System(notificationForwarding, "Notification Forwarding", "Notifies customers and experts via e-mail or sms on specific events")

Rel(customer, ticketInput, "Enters new problem tickets")
Rel(customer, customerProfile, "Maintains profile, contracts and billing information")
Rel(customer, survey, "Fills in survey")

Rel(notificationForwarding, customer, "Sends E-mail/SMS")
@enduml

```