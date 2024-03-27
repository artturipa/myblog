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



### Roles
Roles sn_grc.ROLE_NAME are legacy roles, now they are separated. Legacy roles are contained in new roles. For example both sn_compliance.user and and_risk.user contain sn_grc.user.

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


### Compliance Score Calculations

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

**Indicator** 

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


**Risk Lifecycle**


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

## Roles

Compliance Manager and Risk Manager can create:
* Entities, Entity classes and Entity types
* Issues, Indicators, Remediation Tasks and Policy Exceptions

Compliance Managers can create:
* Policies 
* Control Objectives (sometimes referred as Policy Statements)
* Policy Exceptions
* Controls
* Authority Documents
* Citations

Risk Managers can create:
* Risks
* RIsk Frameworks
* Risk Statements

Risk Managers and Risk users can:
* View
    * Risk Frameworks, Risk statements, Assessments, and Risk Response Tasks
* Create
    * Risks

## Tables

### Tips and specifics
* Most base tables start with **sn_grc_**, and extended tables with **sn_**
* SOX Content pack can be acquired via Store

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


