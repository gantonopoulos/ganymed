Ticket Input Container

```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml


Person_Ext(customer, "Customer", "A customer of the service with a subscription")

Container_Boundary(ticketInput, "Ticket Input"){
    Component(ticketInput1, "Ticket-Input\nMicroservice 1", "", "Handles the ticket creation from the customer")
    Component(ticketInput2, "Ticket-Input\nMicroservice 2", "", "Handles the ticket creation from the customer")
    Component(ticketInputN, "Ticket-Input\nMicroservice N", "", "Handles the ticket creation from the customer") 
    ComponentDb(ticketInput1DB, "Microservice 1 DB", "", "Customer and contract data copy")
    ComponentDb(ticketInput2DB, "Microservice 2 DB", "", "Customer and contract data copy")
    ComponentDb(ticketInputNDB, "Microservice N DB", "", "Customer and contract data copy")
    ComponentQueue(Broker, "Load Balancer", "","Balances the load of new ticket transmission")

    Rel_D(ticketInput1DB, ticketInput1,"Read customer data")
    Rel_D(ticketInput2DB, ticketInput2,"Read customer data")
    Rel_D(ticketInputNDB, ticketInputN,"Read customer data")
        
    Rel(ticketInput1,Broker, "Enqueue new Ticket")
    Rel(ticketInput2,Broker, "Enqueue new Ticket")
    Rel(ticketInputN,Broker, "Enqueue new Ticket")    
}
Container(ticketProcessor, "Ticket Processing", "Service", "Handles the open ticket's lifecycle after creation, until its completion")    

Rel_L(customer,ticketInput1, "Create problem ticket")
Rel_D(Broker, ticketProcessor,"Dequeue and transmit next ticket")

SHOW_LEGEND(false)
@enduml
```