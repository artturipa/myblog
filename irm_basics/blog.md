# ServiceNow IRM in a nutshell
This is yet in progress. But I need this so hence already posted to the site.

### Essential Classes in the Data Model

#### Entity
*sn_grc_profile*

Objects whose exposure must be managed. Such as location, businesses, locations, processes, people, or anything... Risks and controls and audits relate to entities.

#### Entity Class
*sn_grc_profile_class*

Classify entities. Are not related to entity types, but to entities themselves. Entity classes are used to tag different entities and are useful in reporting. Entities can have multiple entity classes.

#### Entity Type
*sn_grc_profile*

Classify entities, type is used in scoping (risk statements and control objectives) and has a lot of significance. Only one type for entity.

#### Issue
*sn_grc_issue*

Generic issue, for example an operational risk event, compliance violation, security breach etc. ServiceNow does not provide detailed issue workflow, so customers are free to implement structure that fits them.

#### Risk event
*sn_risk_advanced_event*

Potential or actual losses and near misses.

#### Risk Response Task
*sn_risk_response_task*

Parent class of different types of tasks that are used to respond to risks. Child classes below.

##### Risk Acceptance 
*sn_risk_acceptance_task*

##### Risk Event Task
*sn_risk_advanced_mitigation_task*

##### Risk Avoidance
*sn_risk_avoidance_task*

##### Risk Mitigation
*sn_risk_mitigation_task*

##### Risk Transfer
*sn_risk_transfer_task*

