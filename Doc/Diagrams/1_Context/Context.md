```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml


Person_Ext(customer, "Customer", "A customer of the service with a subscription")
Person_Ext(customer_1, "Customer", "A customer of the service with a subscription")
Person(sysopsExpert,"Expert", "Qualified personnel carrying out repairs on the customer site")
Person(sysopsAdmin, "Administrator", "Maintainer of internal system data")
Person(manager, "Manager", "Observer of the system's operation and performance")

System(notificationForwarding, "Notification Forwarding", "Notifies customers and experts via e-mail or sms on specific events")
System(sysopsManager, "Sysops Maintenance", "Maintains the user, expert and management info")
System(customerProfile,"Customer Profile", "Maintains the customer data and activities")
System(billing, "Billing", "Maintains contract and billing data and initiates payments periodically")
System(reporting, "Reporting","Requests data from other systems to produce reports")
System(knowledgeBase,"Knowledge Base", "Maintains and provides access to the knowledge articles the experts create")
System(survey, "Survey", "Maintains the customer surveys and keeps track of their progress")
System_Ext(payment, "Payment", "Executes billing mandates")
System(ticketManagement, "Ticket Manager", "Handles the problem ticket lifecycle")

Rel_D(manager, reporting, "Requests report generation")
Rel_D(reporting, ticketManagement, "Gets data")
Rel_D(reporting, customerProfile, "Gets data")
Rel_R(reporting, sysopsManager, "Gets data")
Rel_R(reporting, billing, "Gets data")
Rel_D(reporting, survey, "Gets data")

Rel_R(billing, payment, "Executes recurring payment")
Rel_L(payment, billing, "Informs about payment outcome")
Rel_U(survey, customerProfile, "Gets customer data")
Rel_U(survey, ticketManagement, "Gets ticket status")
Rel_D(survey, notificationForwarding, "Requests pending survey notification to customer")
Rel_D(notificationForwarding, customer_1, "Sends E-mail/SMS")

Rel_D(ticketManagement, notificationForwarding, "Sends expert assignment notifications")
Rel_R(notificationForwarding, sysopsExpert, "Sends SMS")

Rel_R(sysopsExpert, knowledgeBase, "Reads and Edits technical articles")
Rel_U(knowledgeBase, sysopsManager, "Gets author data")
Rel_U(knowledgeBase, ticketManagement, "Gets ticket data")

Rel_D(customer, ticketManagement, "Enters new problem tickets")
Rel_D(customer, customerProfile, "Maintains profile, contracts and billing information")
Rel_D(customer, survey, "Fills in survey")
Rel_U(billing, customerProfile, "Gest customer data")


Rel_L(customerProfile, ticketManagement, "Gets ticket data")
Rel_U(sysopsAdmin, sysopsManager, "Uses")
Rel_D(sysopsAdmin, billing, "Manages")


SHOW_LEGEND(false)
@enduml

```



