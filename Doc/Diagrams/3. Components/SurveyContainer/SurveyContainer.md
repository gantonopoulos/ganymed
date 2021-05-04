Survey Container

```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml



ContainerDb(centralDb, "Central Database", "", "Persists all customer, sysops user, survey, contact and billing data")
System(ticketManagement, "Ticket Manager", "Handles the problem ticket lifecycle")
Container(userApp, "Single-Page Application", "", "Provides the frontend to the customer to submit a survey")
System(notificationForwarding, "Notification Forwarding", "Notifies customers and experts via e-mail or sms on specific events")

Container_Boundary(surveyService,"Survey Service"){
    Component(surveyManager, "Survey Manager", "", "Manages the surveys stored or pending in the system")
    Component(ticketCompletionTracker, "Ticket Completion Tracker", "", "Periodically checks for tickets with state complete for which no survey has been submitted")
    Component(notificationInitiator, "Pending Survey Notifier", "", "Initiate the customer notification process")
}

Rel_D(userApp, surveyManager, "Fills in survey")
Rel_D(surveyManager, centralDb, "Accesses")
Rel_D(ticketCompletionTracker, ticketManagement, "Polls for newly completed tickets")
Rel_L(ticketCompletionTracker, notificationInitiator, "Notify customer survey pending")
Rel_D(notificationInitiator, notificationForwarding, "Send notification")
Rel_R(ticketCompletionTracker, surveyManager, "Get survey data")

SHOW_LEGEND(false)
@enduml

```