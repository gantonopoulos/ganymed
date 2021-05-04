SysOps Maintenance System

```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml

Person(sysopsAdmin, "Administrator", "Maintainer of internal system data")
System(reporting, "Reporting","Requests data from other systems to produce reports")
System(knowledgeBase,"Knowledge Base", "Maintains and provides access to the knowledge articles the experts create")
System_Boundary(sysopsMaintenanceSystem, "Sysops Maintenance"){
    Container(sysopsMaintainer, "SysOps Maintenance", "", "Maintains the SysOps-user, expert and manager info")
    ContainerDb(centralDb, "Central Database", "", "Persists all customer, sysops user, survey, contact and billing data")
    Container(userApp, "Single-Page Application", "", "Provides the frontend to the administrator")
}

Rel_D(sysopsAdmin, userApp, "Uses")
Rel_D(userApp, sysopsMaintainer, "Manages")
Rel_R(sysopsMaintainer, centralDb, "Accesses")
Rel_U(reporting, sysopsMaintainer, "Makes API call to request data")
Rel_U(knowledgeBase, sysopsMaintainer, "Makes API call to request author data")

SHOW_LEGEND(false)
@enduml

```