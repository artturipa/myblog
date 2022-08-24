# ServiceNow IRM in a nutshell
This is yet in progress. But I need this so hence already posted to the site.

### Essential Classes in the Data Model

#### Entity
__sn_grc_profile__

Objects whose exposure must be managed. Such as location, businesses, locations, processes, people, or anything... Risks and controls and audits relate to entities.

#### Entity Class
__sn_grc_profile_class__

Classify entities. Are not related to entity types, but to entities themselves. Entity classes are used to tag different entities and are useful in reporting. Entities can have multiple entity classes.

#### Entity Type
__sn_grc_profile__

Classify entities, type is used in scoping (risk statements and control objectives) and has a lot of significance. Only one type for entity.

#### Issue
__sn_grc_issue__

Generic issue, for example an operational risk event, compliance violation, security breach etc. ServiceNow does not provide detailed issue workflow, so customers are free to implement structure that fits them.

#### Risk event** - Potential or actual losses and near misses.

#### Risk Response Task
__sn_risk_response_task__

Parent class of different types of tasks that are used to respond to risks. Child classes below.

##### Risk Acceptance 
__sn_risk_acceptance_task__

##### Risk Event Task
__sn_risk_advanced_mitigation_task__

##### Risk Avoidance
__sn_risk_avoidance_task__

##### Risk Mitigation
__sn_risk_mitigation_task__

##### Risk Transfer
__sn_risk_transfer_task__

