# ServiceNow IRM in a nutshell
I am studying for a certification exam. Here my notes.

## Definitions

### Entity
* **Entity Filter** filters entities from source table, such as Companies from core_company
* **Entity Type** is to connect risk statements and control objectives to specific types of entities, such as "vendors".
* **Entity Type** [sn_grc_profile_type] and **Entity** [sn_grc_profile] have many to many relationship between them [sn_grc_m2m_profile_profile_type].
* **Entity Classes** [sn_grc_profile_class] classify entities. They are used to tag entities, add business context and organisation for reporting.

### ARA - Advanced Risk Assessment
Differs from Classic risk assessment via:
* Statement hierarchy: ARA has mulstiple levels
* Risk Rollup: Classic risk has none
* Assessment: In ARA scoped risks and objects can be assessed, question types are more various and multiple risk scoring systems are available. 

Risk Framework **is not** relevant when using ARA. Risk values do not rollup to the framework.

### RAM - Risk Assessment Methodology
RAM can be simulated when it is in a draft state and its assessment tyeps are published. When RAM is published, simulations are deleted.

### Compliance Score Calculation
Is calculated for Control Objective. Control Objective can be related to citation (from regulation) or to Policy. Formula for the calculation considers all controls per entities that use the control:

Formula: Sum of weight of compliant controls / Sum of weight of all controls * 100

### Policy Acknowledgement Campaing
* Lifecycle
    * New
    * Pending acknowledgement
    * Closed
    * cancalled

### Policy Exception
Can be requested via 
* Self-service > Employee Center
* Compliance Workspace
* Policy Exceptions module
* From control objective record
* From issue record

Other applications can register policy exceptions with the **Integration Registry**. Integration Registry is a module in Policy and Compliance > Policy Exceptions > Integration Registry. Integration Registry guides developer how Policy Exceptions can be requested from other application.

**Indicator** 

## Lifecycles

## Roles

## Tables

### Tips
* Most base tables start with **sn_grc_**, and extended tables with **sn_**

### Main Tables
* Document [sn_grc_document] [GRC: Profiles] is extended by:
    * Authority Document [GRC: Policy & Compliance]
    * Policy [GRC: Policy & Compliance]
    * Risk Framework [GRC: Risk Management]
* Content [sn_grc_content] [GRC: Profiles] is extended by:
    * Control Objective [GRC: Policy and Compliance]
    * Citation [GRC: Policy and Compliance]
    * Risk Statement [GRC: Risk Management]
* Item [sn_grc_item] [GRC: Profiles] is extended by:
    * Control [GRC: Policy and Compliance]
    * Risk [GRC: Risk Management]


## 



## Essential Classes in the Data Model

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

### Risk

#### Risk
*sn_risk_risk*

a Risk, relates to entity and risk statement. Extends Control/Risk *sn_grc_item* table. Risks have a following standard lifecycle: Draft - Assess - Respond - Review - Monitor - Retired.

#### Risk Statement

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

### Compliance

#### Control Objective
*sn_compliance_policy_statement*

Control objective that does not relate to any individual entity, but to one or many entity types. Control objective holds the information on what type of questionnaire (Attestation) to use.

#### Controls
*sn_compliance_control*

Controls, created separately for individual entities. Relates to Entity and Control Objective. Extends Control/Risk *sn_grc_item* table. Risks have a following standard lifecycle: Draft - Attest - Review - Monitor - Retired.

#### Control Attestation
*asmt_assessment_instance*

a test in a form of questionnaire, which tests whether an individual control is implemented. Actually exists in assessment instance table.

#### Control Test
*sn_audit_control_test*

a test, which tests whether an individual control is effective from design and operational standpoint. 

Control test does not include an questionaire / assessment functionality. Filling the information is intended for fulfiller users.

### Audit

#### Plans
*sn_audit_advanced_plan*

Used to plan audits and engagements, scope the audits correctly and ensure that costs are kept in control.

#### Auditable units
*sn_audit_advanced_auditable_unit*

#### Engagements
*sn_audit_engagement*

a project like structure, which is used to conduct an audit.

#### Audit tasks
*sn_audit_task*

Generic tasks which are completed throughout an engagement.

#### Test plans
*sn_audit_test_plan*

Used to describe how a feature is to be tested. References a control.


