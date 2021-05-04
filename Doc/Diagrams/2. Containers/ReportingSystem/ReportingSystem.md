Reporting System

```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml


System(ticketManagement, "Ticket Manager", "Handles the problem ticket lifecycle")
Person(manager, "Manager", "Observer of the system's operation and performance")
System_Boundary(reportingSystem, "Reporting"){
    Container(sysopsMaintainer, "SysOps Maintenance", "", "Maintains the SysOps-user, expert and manager info")
    Container(customerProfile,"Customer Profile", "", "Maintains the customer data and activities")
    Container(billing, "Billing", "", "Maintains contract and billing data and initiates payments periodically")
    Container(survey, "Survey", "", "Maintains the customer surveys and keeps track of their progress")
    Container(userApp, "Single-Page Application", "", "Provides the frontend to the manager to maintain and generate reports")
    Container(reporting, "Reporting","", "Requests data from other systems to produce reports")    
}

Rel_D(manager,userApp,"Uses")
Rel_D(userApp,reporting,"Maintains")
Rel(reporting, billing,"Makes API calls")
Rel(reporting, survey,"Makes API calls")
Rel(reporting, customerProfile,"Makes API calls")
Rel(reporting, sysopsMaintainer,"Makes API calls")
Rel(reporting, ticketManagement,"Makes API calls")



SHOW_LEGEND(false)
@enduml

```