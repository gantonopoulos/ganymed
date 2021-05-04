Billing Container

```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml


System_Ext(payment, "Payment", "Executes billing mandates")
Container(userApp, "Single-Page Application", "", "Provides the frontend to the administrator")
ContainerDb(centralDb, "Central Database", "", "Persists all customer, sysops user, survey, contact and billing data")
Container_Boundary(billingService,"Billing Service"){
    Component(billingDataManager,"Billing Data Manager","","Maintains all billing and contract data")    
    Component(billingWatchDog,"Subscription Watchdog","","Monitors for subscription fees that require to be paid")
    Component(paymentSession, "Payment Session", "Initiates a session for charging a subscription fee")
}

Rel_D(userApp,billingDataManager,"Calls")
Rel_D(billingDataManager, centralDb,"Accesses")
Rel_L(billingWatchDog, billingDataManager,"Get contract data")
Rel_U(billingWatchDog, paymentSession,"Notify payment due")
Rel_U(paymentSession, payment, "Executes recurring payment")
Rel_D(payment, paymentSession, "Informs about payment outcome")
Rel_D(paymentSession, billingDataManager, "Change subscription payment state")


SHOW_LEGEND(false)
@enduml

```