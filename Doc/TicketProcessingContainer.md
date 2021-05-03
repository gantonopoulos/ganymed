Ticket Processing Container

```plantuml

@startuml 
!include Lib\C4.puml
!include Lib\C4_Context.puml
!include Lib\C4_Container.puml
!include Lib\C4_Component.puml



Person(sysopsExpert,"Expert", "Qualified personnel carrying out repairs on the customer site")
System(supportMainframe, "Customer support mainframe", "Contains all customer, billing and sysops user data")
Container(mobileApp, "Mobile App", "", "Provides the expert access to the ticket and knowledge base systems")
Container(ticketInput, "Ticket Input", "MicroServices", "Handles the ticket creation from the customer")
System(notificationForwarding, "Notification Forwarding", "Notifies customers and experts via e-mail or sms on specific events")

Container_Boundary(ticketProcessing, "Ticket Processing" ,"Handles the open ticket's lifecycle after creation, until its Completion"){
    Component(ticketMaintenance, "Ticket Maintenance", "", "Maintains the ticket records")    
    Component(ticketAssigner, "Ticket Assignment", "", "Processes expert information to decide to which expert to assign tickets")    
    Component(sysopsExpertLocator, "Expert Location Tracking", "", "Receives the current location of the experts")
    Component(ticketProgress, "Ticket Progress Tracking", "", "Periodic checker of open ticket state")    
    ComponentDb(ticketDb, "Ticket DB", "", "Contains ticket related data")

    Rel_D(ticketAssigner, ticketProgress, "Update ticket state")
    Rel_D(ticketMaintenance, ticketDb, "Uses")
    Rel_U(ticketProgress, ticketAssigner, "Request assignment")
    Rel(ticketProgress, ticketMaintenance, "Read/write ticket data")

    Lay_R(ticketMaintenance, sysopsExpertLocator)
    Rel_L(ticketAssigner, sysopsExpertLocator, "Get expert location")
}

Rel_D(sysopsExpert,mobileApp, "Uses")
Rel_D(mobileApp, ticketMaintenance,"Gets or sets (accept/reject/complete) ticket data")
Rel_R(ticketInput, ticketMaintenance, "Send new ticket")
Rel_L(ticketMaintenance, ticketInput, "Response to new ticket")
Rel_R(ticketAssigner, supportMainframe, "Requests expert data", "API Call")
Rel_D(mobileApp, sysopsExpertLocator, "Reports expert location")
Rel_D(ticketAssigner, notificationForwarding, "Sends expert assignment notifications")


SHOW_LEGEND(false)
@enduml
