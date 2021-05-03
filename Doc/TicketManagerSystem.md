Ticket Manager Container

```plantuml

@startuml 
!include Lib\C4.puml
!include Lib\C4_Context.puml
!include Lib\C4_Container.puml
!include Lib\C4_Component.puml


Person_Ext(customer, "Customer", "A customer of the service with a subscription")
Person(sysopsExpert,"Expert", "Qualified personnel carrying out repairs on the customer site")
System(notificationForwarding, "Notification Forwarding", "Notifies customers and experts via e-mail or sms on specific events")

System_Boundary(ticketManagement, "Ticket Manager"){
    Container(ticketInput, "Ticket Input", "MicroService", "Handles the ticket creation from the customer")
    Container(ticketProcessor, "Ticket Processing", "Service", "Handles the open ticket's lifecycle after creation, until its completion")        
    Container(mobileApp, "Mobile App", "", "Provides the expert access to the ticket and knowledge base systems")

    Rel(ticketInput, ticketProcessor, "Sends new tickets")
    Rel(ticketProcessor,ticketInput, "Responds to ticket")
    Rel(ticketProcessor, ticketDb, "Uses")
    Rel(sysopsExpert,mobileApp, "Uses")
}

Rel_R(customer, ticketInput, "Enters new problem tickets")
Rel_L(mobileApp, ticketProcessor, "Reads ticket information")
Rel_L(mobileApp, ticketProcessor, "Reports location")
Rel(ticketProcessor, notificationForwarding, "Sends expert assignment notifications")

SHOW_LEGEND(false)
@enduml
