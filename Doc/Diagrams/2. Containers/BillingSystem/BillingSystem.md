Billing System

```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml


System(reporting, "Reporting","Requests data from other systems to produce reports")
System(customerProfile,"Customer Profile", "Maintains the customer data and activities")
System_Ext(payment, "Payment", "Executes billing mandates")
Person(sysopsAdmin, "Administrator", "Maintainer of internal system data")
System_Boundary(billingSystem,"Billing"){
    Container(billing,"Billing Service","","Maintains contract and billing data and initiates payments periodically")
    Container(userApp, "Single-Page Application", "", "Provides the frontend to the administrator")
    ContainerDb(centralDb, "Central Database", "", "Persists all customer, sysops user, survey, contact and billing data")
}

Rel_D(sysopsAdmin, userApp, "Uses")
Rel_D(userApp, billing, "Calls")
Rel_U(reporting, billing, "Makes API call to request data")
Rel_D(billing, customerProfile, "Gest customer data")
Rel_L(billing, centralDb, "Accesses")
Rel_R(billing, payment, "Executes recurring payment")
Rel_L(payment, billing, "Informs about payment outcome")


SHOW_LEGEND(false)
@enduml

```