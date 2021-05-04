System Context 

```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml

Person_Ext(customer, "Customer", "A customer of the service with a subscription")
Person(sysopsExpert,"Expert", "Qualified personnel carrying out repairs on the customer site")
Person(sysopsAdmin, "Administrator", "Maintainer of internal system data")
Person(sysopsManager, "Manager", "Observer of the system's operation and performance")

System(ticketManagement, "Ticket Manager", "Handles the problem ticket lifecycle")
System(supportMainframe, "Customer support mainframe", "Contains all customer, billing and sysops user data")
System(notificationForwarding, "Notification Forwarding", "Notifies customers and experts via e-mail or sms on specific events")
System(knowledgeBase,"Knowledge Base", "Maintains and provides access to the knowledge articles the experts create")
System_Ext(payment, "Payment", "Executes billing mandates")

Rel(customer, ticketManagement, "Enters new problem tickets")
Rel(customer, supportMainframe, "Maintains profile, contract, transaction and billing information")

Rel(sysopsAdmin, supportMainframe, "Manages")

Rel(sysopsManager, supportMainframe, "Requests report generation")

Rel(sysopsExpert, knowledgeBase, "Reads and edits technical articles")
Rel(sysopsExpert, ticketManagement, "Reads ticket information and reports location")

Rel(notificationForwarding, customer, "Sends E-mail/SMS")
Rel(notificationForwarding, sysopsExpert, "Sends SMS")

Rel(ticketManagement, notificationForwarding, "Sends expert assignment notifications")
Rel(ticketManagement, supportMainframe, "Requests expert data")
Rel(supportMainframe, notificationForwarding, "Send survey notification")
Rel(supportMainframe, payment, "Executes recurring payment")

Rel(payment, supportMainframe, "Informs about payment outcome")

Rel(knowledgeBase, supportMainframe, "Gets expert data")


SHOW_LEGEND(false)
@enduml

```


