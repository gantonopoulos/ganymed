# ganymed Team 

# Architectural Kata

## Solution overview

In our solution we focused mostly on resolving the elasticity problem of the system, which was causing problem tickets to be lost or wrongly assigned. We also tackled the rigidity of the overall system, with regard to change, which made fixing existing and emerging bugs unfeasible.
Our overall approach is explained in the [SystemOverview](Doc/Adr/SystemOverview.md) ADR.

## Documenting
To document our solution we employed the C4 Architectural documentation model. We used [PlantUML](https://plantuml.com/) and the [C4 Plant UML stdlib](https://github.com/plantuml-stdlib/C4-PlantUML) to prepare the diagrams.

# Table of Contents
* [Context Diagram](#context-diagram)
* [Container/Component Diagrams](#container-diagrams)
    * [Ticket Manager System](#Ticket-Manager-System)
        * [Ticket Processing Container](#Ticket-Processing-Container)
        * [Ticket Input Container](#Ticket-Input-Container)
    * [Billing System](#Billing-System)
        * [Billing Container](#Billing-Container)
    * [Customer Profile System](#Customer-Profile-System)
    * [Knowledge Base System](#Knowledge-Base-System)
    * [Notification Forwarding System](#Notification-Forwarding-System)
        * [Notification Forwarding Container](#Notification-Forwarding-Container)
    * [Reporting System](#Reporting-System)
    * [Survey System](#Survey-System)
        * [Survey Container](#Survey-Container)
    * [SysOps Maintenance System](#SysOps-Maintenance-System)
    

## Context Diagram
Below is the context diagram of our solution. Customer actor is displayed on multiple locations to help the drawing algorithm.
Each of the displayed Systems, along with its Components where applicable, will be elaborated in the following sections.
![Context Diagram](Doc/Diagrams/1_Context/Context.png)

## Container/Component Diagrams

### Ticket Manager System 

![Ticket Manager](Doc/Diagrams/2_Containers/TicketManagerSystem/TicketManagerSystem.png)

#### Ticket Processing Container
![Ticket Processing Container](Doc/Diagrams/3_Components/TicketProcessingContainer/TicketProcessingContainer.png)

#### Ticket Input Container

Here lies the core of our solution. In the [Ticket System](Doc/Adr/TickectSystem.md) and [Ticket Input Datatables](Doc/Adr/TicketInputDatatables.md) ADRs you can read about the rationale behind choosing the micro-service architecture for the ticket input process, as well about the micro-service database content.

![Ticket Input Container](Doc/Diagrams/3_Components/TicketInputContainer/TicketInputContainer.png)

### Billing System
![Billing System](Doc/Diagrams/2_Containers/BillingSystem/BillingSystem.png)

#### Billing Container
![Billing Container](Doc/Diagrams/3_Components/BillingContainer/BillingContainer.png)

### Customer Profile System
![Customer Profile](Doc/Diagrams/2_Containers/CustomerProfileSystem/CustomerProfileSystem.png)

### Knowledge Base System
We decided to move the knowledge base system to a dedicated service with a dedicated database. The rational is explained in the [Knowledge Base Service](Doc/Adr/KnowledgeBaseService.md) ADR.

![Knowledge Base System](Doc/Diagrams/2_Containers/KnowledgeBaseSystem/KnowledgeBaseSystem.png)

### Notification Forwarding System

![Notification Forwarding System](Doc/Diagrams/2_Containers/NotificationSystem/NotificationSystem.png)

#### Notification Forwarding Container

![Notification Forwarding Container](Doc/Diagrams/3_Components/TicketInputContainer/TicketInputContainer.png)

### Reporting System

![Reporting System](Doc/Diagrams/2_Containers/ReportingSystem/reportingSystem.png)

### Survey System

![Survey System](Doc/Diagrams/2_Containers/SurveySystem/SurveySystem.png)

#### Survey Container

![Survey Container](Doc/Diagrams/3_Components/SurveyContainer/SurveyContainer.png)

### SysOps Maintenance System

![SysOps Maintenance System](Doc/Diagrams/2_Containers/SysOpsMaintenanceSystem/SysOpsMaintenanceSystem.png)

