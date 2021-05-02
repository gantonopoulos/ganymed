```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml


Person_Ext(customer, "Customer", "A customer of the service with a subscription")
Person(sysopsExpert,"Expert", "Qualified personnel carrying out repairs on the customer site")
Person(sysopsAdmin, "Administrator", "Maintainer of internal system data")
Person(manager, "Manager", "Observer of the system's operation and performance")

System(notificationForwarding, "Notification Forwarding", "Notifies customers and experts via e-mail or sms on specific events")
System(ticketInput, "Ticket Input", "Handles the ticket creation from the customer")
System(ticketing, "Ticketing", "Handles the open ticket's lifecycle after creation, to completion")
System(sysopsManager, "Sysops Maintenance", "Maintains the user, expert and management info")
System(customerProfile,"Customer Profile", "Maintains the customer data and activities")
System(billing, "Billing", "Maintains contract and billing data and initiates payments periodically")
System(reporting, "Reporting","Requests data from other systems to produce reports")
System(knowledgeBase,"Knowledge Base", "Maintains and provides access to the knowledge articles the experts create")
System(survey, "Survey", "Maintains the customer surveys and keeps track of their progress")
System_Ext(payment, "Payment", "Executes billing mandates")


Rel(customer, ticketInput, "Enters new problem tickets")
Rel(customer, customerProfile, "Maintains profile, contracts and billing information")
Rel(customer, survey, "Fills in survey")

Rel(ticketInput, ticketing, "Submits new problem ticket")

Rel(survey, notificationForwarding, "Requests pending survey notification to customer")
Rel(survey, customerProfile, "Gets customer data")
Rel(survey, ticketing, "Gets ticket status")

Rel(ticketing, sysopsManager, "Reads expert data")
Rel(ticketing, notificationForwarding, "Sends expert assignment notifications")

Rel(manager, reporting, "Requests report generation")
Rel(reporting, ticketing, "Gets data")
Rel(reporting, customerProfile, "Gets data")
Rel(reporting, sysopsManager, "Gets data")
Rel(reporting, billing, "Gets data")

Rel(sysopsAdmin, sysopsManager, "Uses")
Rel(sysopsAdmin, billing, "Manages")

Rel(billing, payment, "Executes recurring payment")
Rel(payment, billing, "Informs about payment outcome")
Rel(sysopsExpert, knowledgeBase, "Reads and Edits technical articles")

Rel(notificationForwarding, customer, "Sends E-mail/SMS")
Rel(notificationForwarding, sysopsExpert, "Sends SMS")

SHOW_LEGEND(false)
@enduml

```



