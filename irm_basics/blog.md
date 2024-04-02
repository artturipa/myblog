# ServiceNow IRM in a nutshell
I am studying for a certification exam. Here my notes.

Glanced flashcards:
https://quizlet.com/484558881/servicenow-grc-risk-and-compliance-cis-flash-cards/  (50 in)


## Common elements

### Entity
* **Entity Filter** filters entities from source table, such as Companies from core_company
* **Entity Type** is to connect risk statements and control objectives to specific types of entities, such as "vendors".
* **Entity Type** [sn_grc_profile_type] and **Entity** [sn_grc_profile] have many to many relationship between them [sn_grc_m2m_profile_profile_type]. One entity can have **multiple** Entity types
* **Entity Classes** [sn_grc_profile_class] classify entities. They are used to tag entities, add business context and organisation for reporting.

Entities, Entity classes and Entity types can be created by roles Compliance Manager and Risk Manager

## Abbrevations

* **SLE** - Single Loss Expectancy
* **ARO** - Annualized Rate of Occurrence
* **Annualized Loss Expectancy** - ALE

(Quantitative Calculation: SLE x ARO = ALE)

## Risk Management

### Risk Framework
is a formalized process for managing risk. Risk frameworks are used by **risk managers** to group risk statements into manageable categories.

### Risk Criteria
is a quantitative or qualitative value against which level of risk is. Risk criteria is required for the risk heatmap.

Risk Assessment questions are known as **factors**:
* Manual factors require human responses
* Automated factors fetch data from ServiceNow
* Group factors can be manual or automated, they are grouped to create a combinated score
* Factor contribution type can be qualitative, quantitave or both

After risk assessment is completed, comes the response. There are four types of response:
* Acceptance
* Avoidance
* Mitigation
* Transfer (Shifting the responsibility or impact of a risk to a third party, for example insurance company)

### ARA - Advanced Risk Assessment
Differs from Classic risk assessment via:
* Statement hierarchy: ARA has mulstiple levels
* Risk Rollup: Classic risk has none
* Assessment: In ARA scoped risks and objects can be assessed, question types are more various and multiple risk scoring systems are available. 

Risk Framework **is not** relevant when using ARA. Risk values do not rollup to the framework.

### RAM - Risk Assessment Methodology
RAM can be simulated when it is in a draft state and its assessment tyeps are published. When RAM is published, simulations are deleted.

## Compliance

### Operational Perspective (example)
1. Policy states that something should be done (__Every employee needs to renew their license annually__)
2. Control is established to ensure compliance with the policy (__Ensure that all employees licenses are up to date__)
3. (Entity) Owners are responsible for enforcing the control in their departemnt
4. Owner declares that they have enforced the contol via **attestation**. Attestation can be a simple form that asks whether the control is in place.
5. Every month, owners deploy their method to enforce the control, results are captured with **indicator** (__Check that license has been confirmed within a month__)
6. Every year, **auditor** confirms that the enforcement of the control works as intended through **Control test**



### Contiunous Monitoring 
Test plans are specific to controls and can be leveraged during audits. Test templates are available

Indicators monitor controls and risks and collect evidence of performance

Control Attestations validate control implementation

### Policy types

**Policy** - Internal practice that must be followed
**Procedure** - Fixed, step-by-step sequence of activities
**Standard** - Documentation of requirements that can be used to ensure that materials/etc are fit for purpose
**Plan** - Documented intended future course of action
**Checklist** - List of items required to be done
**Framework** - Broad overview or outline of interlinked items
**Template** - Pattern for an item or a group of items

### Compliance Score Calculations

**Default hilighting of Control compliance**
* 80+ in green
* 80-50 in yellow
* below 50 in red

__Compliance scoring is the percentage of controls that are compliant for a specific control objective.__

**Control Objective Compliance Score**
Is calculated for Control Objective. Control Objective can be related to citation (from regulation) or to Policy. Formula for the calculation considers all controls per entities that use the control:

Formula: Sum of weight of compliant controls / Sum of weight of all controls * 100

**Profile Score Compliance score**
If property **sn_compliance.cal_score_by_weighted_control** is true

Formula: Sum of weights of all the compliant standard and common controls associated with the entity / sum of weights of all the controls

If the property is false

Formula: Count of all the compliant standard and common controls associated with the entity / Count of all the controls

**Entity Type Compliance Score Calculation**
Average of compliance scores of all the entities under it

**Policy compliance score calculation**
(Average of all immediate policies’ score + Average of all the immediate policy statements’ score) / 2

### Content provider store

**Some Content providers**
* COSO (Committee of Sponsoring Organizations of the Treadway Commission)
* Edgile Automated Regulatory Compliance (ArC)
* FedRamp (Federal Risk and Authorization Management Program)
* HITRUST
* LexisNexis Risk Solutions
* Thomson Reuters
* UCF (United Compliance Framework)
* Wolters Kluwer

Content provider store app consists of:
* Authority documents
* Citations
* Control Objectives from UCF controls
* Relationships between authority documents and citations
* Relationships between citations and control objectives
* Relationships between overlapping authority documents, citations, and control objectives

### Control Types

**Standard Control** have function = Standard Control. There one control is created per entity with name matching control objective.

**Unique Control** have function = Standard Control. There same entity can have additional controls for the control objective, these are unique controls. Control name is different. 

Example: If organization handles multiple products/operational lines, having single control for an entity and control objective might be ineffective.

Unique controls enable high-level controls while allowing more granular controls.

**Common Control** have function = Common Control. Common controls are related to primary entity where the testing occurs. Common control has reliant entities. 

Example: Fire sprinkler system can be a common control for multiple business units.

Function of control affects calculation method. All active, associated common controls contribute to the compliance score.

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

### Consolidated attestation
Allows grouping control attestation

### Indicator 
Indicators are used to measure if a control is effective or not. They are the manual or automated steps that measure effectiveness of the process identified in control attestation.

Indicators can be created using indicator templates which can automatically generate indicators for multiple controls that reference the same control objective.

* Control attestations answer the question, “Has the control been implemented?”
* Indicators answer the question, “Is the control effective?”
* Control tests answer the question, “Is the control effective from a design and operation standpoint?”

## Audit

**Audit Plan** helps managing different types of audits in a periodic manner. Audit engagement is an audit project.

**Engagements hold following types of tasks**
* Control tests
* Interviews
* Walkthroughs
* Activities (=generic tasks)

Audit engagements are scoped with auditable units or entities. Scoping automatically asssociates engagement with:
* All risks related to the entity
* All controls related to the entity
* All test plans related to the controls
* All indicator results related to the controls

## Lifecycles

**Policy Lifecycle**
1. Draft
2. Review (only reviewer can move to the next state)
3. Awaiting Approval (if no approvers defined, policy goes straight to published)
4. Published
5. Retired

**Control Lifecycle**
1. Draft
2. Attest
3. Review (Here attestations are reviewed by compliance managers)
4. Monitor
5. Retired

**Issue Lifecycle**
1. New
2. Analyze
3. Respond
4. Review
5. Closed

Issues can be automatically created from following scenario:
* Indicator fails
* Attestation results are not implemented
* Control Test effectiveness is ineffective and state of test is closed. (Issues are automatically closed when a control test result failure is remediated.)
* Continuous monitoring results

Issue Workflow:
1. Identification
2. Triage
    * Confirmed as a new issue
    * Confirmed as an existing issue
    * Confirmed as a risk event
    * Track as recommendation
    * Close as non-issue / no action required
3. Identify Owner
4. Evaluation
5. Action Steps
6. Monitor and review

**Risk Lifecycle**
1. Draft
2. Assess
3. Respond
4. Monitor
5. Retired

**Risk Response Lifecycle**
1. Draft
2. Work in Progress
3. Awaiting approval (only if response type = accept)
4. Review
5. Closed

**Policy Exception Lifecycle**
1. New
2. Analyze
3. Risk Assessment
4. Review
5. Awaiting Approval
6. Approved
7. Closed

Policy Exceptions can be created from:
* Policy Exception module
* Issues
* Policy Statement
* Policy

**Regulatory feed lifecycle**
1. New
2. Impact assessment
3. In progress
4. Deferred
5. Cancelled
6. Closed

__When a regulatory feed type of event is marked as applicable, a regulatory change task is automatically created. For a source document type of feed, a source document import task is automatically created.__

**Regulatory change task lifecycle**
1. New
2. Respond
3. Awaiting approval
4. Implementation
5. Closed

**Source document import task lifecycle**
1. Ready to import
2. In progress
3. Awaiting approval
4. Implementation (optional)
5. Closed 

**Audit Engagement Lifecycle**
1. Scope
2. Validate & Plan
3. Fieldwork
4. Awaiting approval
5. Follow-up
6. Closed

## Roles

Roles sn_grc.ROLE_NAME are legacy roles, now they are separated. Legacy roles are contained in new roles. For example both sn_compliance.user and and_risk.user contain sn_grc.user.

Risk and compliance roles both have levels admin, manager, user, reader. In addition to those, compliance has role **Compliance Developer** [sn_compliance.developer] (contains Compliance Admin). Roles with higher access contain role with lower access.

**GRC business user lite** [sn_grc.business_user_lite] can:
* Read and update if assigned to them:
    * Policy acknowledgements
    * Control attestations
    * Issues assigned and issue remediation tasks
    * Evidence requests
    * Risk response tasks
    * Manual indicator tasks
* Review and approve AR assessment
* Create, read or update Policy Exceptions

**GRC business user** [sn_grc.business_user] can do all the same, and in addition they can:
* Contribute to policies
* Group attestations
* Request and approve policy exceptions
* Accept work and approve evidence responses
* Assign risk tasks
* Take risk assessments

**Compliance/Risk user** can do all the same, and in addition:
* Compliance user:
    * Create policies, control objectives, controls and policy acknowledgement campaings
    * Request evidence
    * Group Issues
* Risk user:
    * Create risks and risk assessments
    * Relate controls to a risk


### Compliance and Risk

Compliance Manager [sn_compliance.manager]  and Risk Manager [sn_risk.manager] can create:
* Entities, Entity classes and Entity types
* Issues, Indicators, Remediation Tasks and Policy Exceptions

Compliance Managers can create:
* Policies (Compliance users can do this as well)
* Control Objectives (sometimes referred as Policy Statements)
* Policy Exceptions
* Controls
* Authority Documents
* Citations

Risk Managers can create:
* Risks
* Risk Frameworks
* Risk Statements

Risk Managers and Risk users [sn_risk.user] can:
* View
    * Risk Frameworks, Risk statements, Assessments, and Risk Response Tasks
* Create
    * Risks

Compliance users [sn_compliance.user] can:
* Send ou tpolicy acknowledgement campaings
* Schedule and follow-up with attestations
* Respond to indicator task
* Create, manage and review issues
* Request evidence for controls, policies and issues

NOTE that Control owner is a role in operational model, but there is no role in the system besides Compliance user [sn_compliance.user]. Control owners are the ones that manage their controls, it is an attribute of a control record. 

### Regulatory Change Management
**RCM Admin** [sn_grc_reg_change.admin] can:
* Set up the RCM application
* Coordinate and facilitate configuration requests
* Maintain taxonomy values

**RCM IT Admin** [sn_grc_reg_change.it_admin] may often be same individual as the admin. The role can:
* Set up the regulatory intelligence providers in the ServiceNow RCM application

**RCM Manager** [sn_grc_reg_change.manager] can:
* Monitor the progress of regulatory change initiatives within the organization
* View all the regulatory content updates relevant to the organization
* Assign new regulatory feeds that are sourced from external sources
* Assign regulatory tasks within the teams reponsible for managing regulatory change

RCM manager assigns the regulatory change task to RCM User. RCM user has only read access to the task until it is assigned.

**RCM User** [sn_grc_reg_change.user] can:
* Assess the applicability of regulatory feeds to the organization
* Initiate impact assessments and assign them to subject matter experts (SMEs) or owners of the organization
* Complete assigned regulatory tasks
* Create actions tasks for the risk and compliance users to complete

RCM user role is given to individuals that handle responsibilities as Regulatory Change Coordinators.

### Audit 

**Audit Admin** [sn_audit.admin] can:
* Set up the Audit Management application
* Coordinate and facilitate coniguration requests
* Delte engagements, audit tasks, test templates and test plans

**Audit Manager** [sn_audit.manager] can:
* Create audit plans and engagements, including records necessary to conduct the audit, such as milestones, tasks and evidence requests
* Approve audit tasks, workpapers and engagements
* Track and monitor audit findings

**Audit User** [sn_audit.user] can:
* Perform fieldwork (walkthroughs, interviews, control testing, etc.)
* Document the work and findings
* Resolve and/or follow up with audit findings
* Create test templates and test plans
* Read Policy and Compliance and Risk Management Applications

**Engagement project manager** [sn_audit_advanced.engagement_project_manager] can:
* Complete advanced planning with audit plans and engagements
* Create resource and costs plans and approve time cards

**External auditor** [sn_audit.external_auditor]
* Perform audit against specific regulation
* View closed engagements and tasks
* View published policies, controls and risks in the Monitor state

## Tips and specifics
* Most base tables start with **sn_grc_**, and extended tables with **sn_**
* SOX Content pack can be acquired via Store
* Citations can have parent citations

## Tables

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


