Knowledge-Base System

```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml

Person(sysopsExpert,"Expert", "Qualified personnel carrying out repairs on the customer site")
System(sysopsManager, "Sysops Maintenance", "Maintains the user, expert and management info")
System(ticketManagement, "Ticket Manager", "Handles the problem ticket lifecycle")

System_Boundary(knowledgeBaseSystem,"Knowledge-Base"){
    Container(knowledgeBaseManager, "Knowledge-Base Service", "", "Provides access to the knowledge base articles")
    ContainerDb(knowledgeBaseDb, "Knowledge-Base Database", "", "Persists all knowledge base articles created by the sysops experts.")
    Container(userApp, "Mobile Application", "", "Provides the frontend to the expert to access and manage the knowledge base articles")
}

Rel_D(sysopsExpert, userApp,"Uses")
Rel_D(userApp, knowledgeBaseManager, "Calls")
Rel_L(knowledgeBaseManager, knowledgeBaseDb, "Accesses")
Rel_R(knowledgeBaseManager, sysopsManager, "Gets author data")
Rel_D(knowledgeBaseManager, ticketManagement, "Gets ticket data")

SHOW_LEGEND(false)
@enduml

```