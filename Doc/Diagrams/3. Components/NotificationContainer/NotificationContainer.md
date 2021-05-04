Notification Forwarding Container

```plantuml

@startuml 
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Context.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Container.puml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/v2.2.0/C4_Component.puml


Person_Ext(customer, "Customer", "A customer of the service with a subscription")
Person(sysopsExpert,"Expert", "Qualified personnel carrying out repairs on the customer site")
System(ticketManagement, "Ticket Manager", "Handles the problem ticket lifecycle")
System(survey, "Survey", "Maintains the customer surveys and keeps track of their progress")

Container_Boundary(notificationService,"Notification Forwarding"){
    Component(notificationRouter, "Notification Router", "", "Contains the logic of the medium to be used for the pending notification")
    Component(emailNotifier, "E-Mail Notifier", "", "Sends emails to recipients")
    Component(smsNotifier, "SMS Notifier", "", "Sends SMS to recipients")
}

Rel_U(smsNotifier, sysopsExpert,"Sends ticket assignment SMS")
Rel_U(emailNotifier, customer,"Sends survey pending E-Mail")
Rel_U(smsNotifier, customer,"Sends expert on the way SMS")
Rel_U(notificationRouter, smsNotifier,"Request SMS notification")
Rel_U(notificationRouter, emailNotifier,"Request E-Mail notification")
Rel_U(survey, notificationRouter, "Requests pending survey notification to customer")
Rel_L(ticketManagement, notificationRouter, "Sends ticket assignment notifications")

SHOW_LEGEND(false)
@enduml

```