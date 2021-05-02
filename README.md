# ganymed
Architectural Kata


```plantuml

@startuml 
!include Doc\Lib\C4_Context.puml
!include Doc\Lib\\C4_Container.puml
!include Doc\Lib\\C4_Component.puml


Person(administrator, "Admin", "Administrator user")
Person(Customer, "Customer", "")
Person(Expert, "Expert", "")
Person(Manager, "Manager", "")
Person(System, "System", "")

Container(reporting, "Reporting System", "", "")
Container(billing, "Billing System", "", "")

System_Boundary(ticketInput, "Ticket Input"){
    Container(ticketInput1, "Ticket-Input\nMicroservice 1", "", "Handles the ticket creation from the customer")
    Container(ticketInput2, "Ticket-Input\nMicroservice 2", "", "Handles the ticket creation from the customer")
    Container(ticketInputN, "Ticket-Input\nMicroservice N", "", "Handles the ticket creation from the customer") 
    ComponentQueue(Broker, "Ticket-Broker", "","Balances the load of new ticket transmission")

    Lay_R(ticketInput1, ticketInput2)
    Lay_R(ticketInput2, ticketInputN)
    Rel(ticketInput1,Broker, "Enques new Ticket")
    Rel(ticketInput2,Broker, "Enques new Ticket")
    Rel(ticketInputN,Broker, "Enques new Ticket")
    
}

System_Boundary(ticketSystem,"Ticket-Management"){
    Component(completion, "Completion", "", "Handles ticket completion")
}

Lay_D(ticketInput,ticketSystem)

SHOW_LEGEND(false)
@enduml

```