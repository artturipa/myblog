# Framework to facilitate effective security practices

I recently participated to SABSA foundation training. I was pleased by the ideas and concepts the training gave me. 

Below are the notes I did when I trained for the certification exam. The notes give you an overview of the ideas included in the course. The training itself was five full days, and I recommend participating to it in case the topics resonate with you.

[This speech](https://www.youtube.com/watch?v=BwTIpa7oSDY) Gives a good example about benefits of SABSA -approach.

# NOTES

## Concept of Enterprise
Treats organisation as a single entity, not as multiple individual departments. Embraces end to end nature of business processes and avoids local optimisation
## Concept of Security
To provide confidence and assurance. Towards opportunities and risks.
## Concept of Architecture
Supports business strategy, does not cover implementation details as those might change. 
## Role of an architectural framework
Consistent set of policies, principles, capabilities and standards. Sets the direction and vision for the development and operations to ensure alignment with business goals.

Maintains integrity of design in complex developments.

## Sabsa guiding principles, drivers & Constraints
* Architecture must not support any particular Culture, Management, Technologies.
* Architecture must meet ones unique set of business requirements
* Architecture must provide sufficient flexibility.

## How SABSA resolves historical, tactical & siloed approach to Security
Not as much emphasis to technology. Enterprise view. 

## 7 Primary features & Advantages of the SABSA approach to Enterprise Security Architecture
### Features and Advantages
* Business-Driven / Value-assured
* Risk-focused / Priorised & Proportional
* Comprehensive / Scalable scope
* Modular / Agility
* Open Source / Free use, standard
* Auditable / Demonstrates compliance
* Transparent / Two-way traceability

# Section 4 

## SABSA Matrix
### 6 views of SABSA architecture

1. Business View
2. Architect's view
3. Designer's view
4. Builder's view
5. Tradesman's view
6. Manager's view

### 6 layers of SABSA architecture matrix

1. Contextual
2. Conceptual
3. Logical
4. Physical
5. Component
6. Management

### 6 Columns of the SABSA matrices

1. Assets (What)
2. Motivation (Why)
3. Process (How)
4. People (Who)
5. Location (Where)
6. Time (When)

### Position of key deliverables in SABSA Matrices

### Describe the overlaying of layer 6 to create the management matrix

6th layer rises to the top, and the other cells explain the management activity related to the cell

## Traceability concept

# Business Context & Requirements

## Traceability flow from business requirements to attributes

## SABSA Attributes

Conceptual abstraction of a business requirement

## Rules and features of attributes

Business Requirements --> Business Drivers for Security --> Attributes

## Attribute taxonomy & Profile

Taxonomy: Name, Definition and Classification

Profile: Taxonomy + Measurement approach, Metric, Performance target

## Elements of attributes requiring customization

Attribute's profile should be customised to reflect local needs & culture.

## Applications & Benefits of the attribute profiling technique

Enables any unique set of business requirements to be engineered as a standardised and re-usable set of specifications.

Attributes require definitions, measurement approach and metric. 

Populates the missing link between business requirement and technology / process design.

# Risk & Opportunity Frameowrk

## Objectives, benefits and applications of Architectured Risk Management

Drivers: Regulation

Aims & Benefits: 
* achieve balance between realising opportunities and minimising losses 
* Establish appropriate infrastructure and culture while applying a systematic method
* Early warnings and fewer surprises
* Economic & Efficient
* Improved planning 
* Accountability assurance & governance

Applications:
* Business planning
* Asset management
* Business Continuity
* Change management
* Liability
* Environmental aspects
* Compliance & Governance
* Procurement 
* Project management

## SABSA Balanced Risk Model

Risk context relates to both positive and negative outcomes. 

Controls protect attribute from negative consequences and Enablers enhance positive consequences for attribute.

## SABSA approach to assess elements of Risk

Impact based approach, focus to "Business critical" and "mission critical" risks. 

In SABSA, operational risk can also be an upside risk.

## Role of attributes performance thresholds in removing subjectivity of risk assessments

Performance target of an attribute provides the threshold for 'acceptable risk'. Failure to meet it is an unacceptable outcome.

This parameter is a key element enabling the assessment to be less subjective. Early warnings are provided by introducing a second risk / performance threshold. 

## SABSA process for compiling business risk management objectives

Risk factor analysis via PESTEL(IM). Compile results to enterprise policies.

## Explain traceable relationship between attributes and controls & enablers

Attributes --> Control Objectives & Enablement Objectives --> Controls & Enablers

## Architectural considerations for creating risk management systems & dashboards

Forecasting problems rather than viewing the history.

# Policy Architecture

Discipline of embedding organisation's objectives into a structured set of documents

## Drivers for, and objectives, benefits & applications of, the SABSA Policy Framework

Policy has multiple iterations and interpreprations. Policy terminology can be varied.

Documentation exists at multiple different levels, and hence it is useful to conceive a hierarchically layered security policy architecture.

Policies are identified as biggest demotivators in the workplaces

Enterprise Policy contains:
1. Contextual policy

2. Conceptual policy

Domain policy contains
3. Logical policy

4. Physical policy

5. Component policy

6. Management Policy


Layers of security policy architecture
* Logical 
** Security Policies & Services
* Physical
** Security Procedures & Mechanism
* Component
** Security Standards & Configurations

## SABSA Policy Framework & its layers and components

Layers: Contextual domain --> Conceptual Domain --> Logical domain --> Physical domain

Columns: Finance Risk, Operational Risk, Environmental Risk, Health & Safety Risk, Information Risk, Etc.

For example:
Business Risk Management Policy --> Information Security Policy --> ICT Security Policy --> Platform Security Policy --> Mobile Device Policy

Logical Domain Policy concept is defined to serve diverse business needs

Policy Authorities - are accountable for the risks and opportunities in their domain

## SABSA Policy Domain concept

Security domain is set of elements subject to a common security policy.

## Policy Domain inter-actions in terms of Risk appetite distribution and risk performance aggregation

The domain policy authority can't do everything himself, so he distributes risk appetite and risk management responsibility to lower level subdomains.

Aggregated performance is reported to higher domains.

Peer domains report to same super domain. Peer domains can delegate to one another.

Higher domain owns aggregated risks and resolves conflicts.

## Issues with multi-dimensional Policy Domain Architectures

Domains (and therefore policies)  can exist in multiple dimensions.
* Logical community domains by business unit and/or geography
* Logical information domain by classification
* Physical infrastructure domain

Multidimensionality is often confusing. Guidance is to draw domain diagrams with single views

## Use of the policy framework & Policy domain concepts to create Enterprise Policy Domain Model

In domain policy hierarchy Commonalities move up, exceptions move down.

# Architectural Strategies

## Objectives of Systems Engineering in SABSA Security Architecture

Inputs --> Black Box --> Outputs

Systems engineering - Systems inside a system

To:
* Manage Complexity
* Top-down decomposition
* Structured thinking
* Peer review
* Communication & documented preservation of ideas

## Subsystems of a Control System

Control Sub-System --> Monitoring & Measurement sub-system --> Decision sub-system

## Concept of integrated Compliance Framework

Aims to provide the framework for compliance with multiple standards simultaneously

Management is built to integrate best practices of the day.

Contextual layer assess and communicates business requirements
Conceptual layer sets strategy for treating risks
Lower layers engineer deployment of controls

## Control Strategies within SABSA architecture

Impact x Likelihood -matrix
* Urgent controls improvement
* Controls improvement
* Active monitoring of KRIs
* Disaster recovery
* Passive monitoring

## SABSA Multi-tiered Control Strategy for defence-in-depth & its control capabilities

SABSA has no controls library, but controls are architected within the framework.

Over-investment in preventative measures results in prevention of business and opportunity.

In SABSA multi-tier: Deter, Prevent, Contain, Detect & Track, Recover, Assure

Depth layering has different controls for different layers:
* Organisational
* Personnel
* Physical
* Hardware
* System Software
* Application Software
* Crypto
* Information Assets

The value of the whole is greater than the sum of its individual parts

Threat --> Domain A -> Domain B - Domain C - Domain D --> Asset
80 / 20 ratio in controls per domain provides significant security

For example add controls to recruitment phase as well as personnel trainings as well as Software application as well as Access Control.

# Role & Responsibility Concept

## Phases & Activities of the SABSA Governance Model

* Strategy and planning, which informs of responsibility to next phase
** Develop strategy & Plans
** Sets goals, objectives, performance targets, risk appetite, Policy to meet targets
* Design
** Design all
* Implement
** Establish processes, implement systems, appoint & train people, Establish controls & enablers
* Manage & Measure
** Manage and monitor

## Roles & Responsibilities in a SABSA RACI Model

All roles must be clearly defined in order to ensure correct and timely decisions.

R - Gets the job done
A - The only person who is accountable
C - The people whose opinions are sought
I - The people who are informed

## Ownership in the SABSA Roles & Responsibilities Model

Ownership is often multifaceted

Ownership of asset, impact, liability.

Ownership type is specific to position in governance model / domain model

Owner is the domain policy authority who sets goals, risk appetite and performance targets

Owner is the one accountable.

Owner can delegate his responsibility to assess risk or mitigate actions, it might be needed if the owner is not competent. Liability does not transfer from owner.

## Roles of trustee & Custodians

Trustee - Responsible as subject matter expert
Custodians - Policy authority is not delegated

## Roles of Service Providers & Customers

## Roles of Compliance & Audit 

Compliance role is appointed by domain authority - informs domain authority

Auditor role is appointed by super domain authority - informs super domain authority

## How SABSA approaches contribute to risk aggregation & reporting

Risk appetite and responsibility is distributed top-down. Subdomains inform about their performance to superdomains

# Domain Concepts

## Benefits of domain models

* Reduces complexity
* Provides agility to integrate business units and technologies
* Forms the location basis for SOA
* Control resources segregation & Enabling information sharing 
* Key to analyze roles and responsibilities

## Domain types

* Superdomain
* Sub domain
* Peer domain (sub domains sharing common superdomain)

* Logical domain constists of logical elements
** LOB, Community of users, Information classification

* Physical domain consists of physical elements (in a physical location or technology layer)
** Territory, site, building, network

## Roles of Registration & Credential issuing authorities

Registration authority
* Sets policy for the domain
* Verifies credentials and establishes identity of applicant
* Establishes right to be registered

Domain certification authority
* Provides chain of trust through hierarchical certifications
* Sets credential issuing policies and practices
* Checks registration and authorisations
* Receives and certifies public keys
* Authenticating credential requests


## Isolated, independent, combined & multi-tiered Domain Models

Isolated domain - No inter-domain associations
Independent domain - Gateway for inter-domain associations
Combined domain - Combines independent or isolated domain with honeycomb domain
- Common in classified systems, for example one security clearance gives access to inter-domain associations

## Inter-domain policy associations

* Through defined gateway
* Between superdomain and subdomain
* Via trusted third party domain
* Through mutually agreed policy

# Time & Performance Management Concept

## 4 Phases of SABSA Lifecycle & relationships between lifecycle and strategic, tactical & operational approaches

Is compatible with "Plan, Do, Check, Act"

Lifecycle:
* Strategy & Planning
* Design
* Implement
* Manage & Measure

Properties of strategic lifecycle
* Strategy
* Tactics
* Operations

SABSA Lifecycle Principles
* Business-driven
* Splits "plan" into "Strategy & Planning" and "Design" to gain better traceablity
* Emphasis on measurement
* Merges "Manage and measure" into one

## Through-life Risk Management Characteristics

* Establish appropriate infrastructure and culture to handle risks in a way that organisations can minimize losses and maximize gains
* Embedded into philosophy, practices and business processes. This way everyone in the organisation becomes involved in the management of risks

## Structure and objectives of SABSA risk management process

* SABSA RMP embodies the SABSA method in a through-life Risk Management process

## Domains and process areas of the SABSA SMP & its objectives

SMP - SABSA Maturity Profile

Based on CMM (Capability Maturity Modelling)

Coordinates SABSA process information from all parts of the process

Idenfities, measures and reports compliance practices

Six SMP Domains
* Contextual Architecture
* Conceptual Architecture
* Logical Architecture
* Physical Architecture
* Component Architecture
* Management Architecture

SMP Maturity levels
* Unrealibity 
* Informal
* Defined
* Monitored
* Optimised

## Process of defining Business-Driven performance targets

Attributes 
--> Measurement Approaches, Performance Metrics, Performance targets
 --> Security Service Level Definition
  --> Stakeholder --> Attributes 

## Architectural vitality

It is the architecture's capacity to live, breathe and adapt its principles, policies, capabilities and standards

# Asset Architecture & Asset Management

Data Assets --> Transformation --> Information Assets

Security is a property of something else (asset)

It is not possible to define security architecture without asset management (=defining assets)

## Characteristics & Deliverables of SABSA Architecture Design Phase layers

Concerned with information security & systems functionality

Elements existing in logical domains are not tied to specific physical locations

* Information assets
* Risk management policies
* Process Maps
* Trust relationships
* Domain maps
* Calendar & Timetable

Component Layer contains specialised tools, brands, protocols

Management architecture is concerned with management processes and activities

## Principles of aligning & integrating SABSA's lower layers with other frameworks

SABSA fills security gaps left by other frameworks.

One should align & enhance, not replace

## Role of SABSA techniques for security in Release & Knowledge mgmt

Change affects assets, and changes might increase or decrease attributes

In KM knowledge is aggregated and contextualised through the SABSA Architecture layers

## Possible start-up approaches to SABSA Enterprise Security Architecture

* Executive Interview 
* Analysis followed by validation
* Fast-track (product)
* Blended approach

# Risk & Policy Management Architecture

Standards are not enough, the contents need to be adapted to unique needs of an organisation

Controls and Enablers can be re-used for various threats and opportunities
--> Re-use standard solutions

## Requirements for architected controls

Traceable control capability

How does one assess effectiviness of control, which control or combination causes best outcome

Elements within each architecture layer are complete, and trace from one layer to the next

## Role in controls architecture of Pure Risk, Appetite thresholds, Acturial Data & Dynamic thresholds

Pure Risk - 100% Vulnerability 100% weakness
Current - Residual risk, which exceeds appetite
Target - All residual risk within appetite

Actuarial data allows predicting target state after control implementation -> Control value assessment
Actuarial data can show results of past control implementations

Dynamic thresholds adapt KRI points based on actuarial information, alert is given at earlier point

## Risk levels, policy levels, control levels & management activities

There are layers (Logical, Physical, Component) covering all:
* Risk Level 
* Policy Level
* Control Level
* Management activity controls

## Structure & objectives of the SABSA assurance framework

Four assurance levels. Assurance levels correlate to risk levels, critical risks need higher level of assurance

Levels might be: Baseline, Special treatment, Defence in depth, Formal Accrediation

# Transformation & Service Architecture

## Concept of top-down process analysis

Process contains sub processes, and so on

Contextual: Meta-Processes consists of
Conceptual: Strategic view of process consists of 
Logical: Information flows & transformations, which consists of
Physical: Data flows & Systems interactions, which consists of
Component: Protocols & Step Sequences

Between process levels exist "Vertical Security Consistency"
Within one process levels are many processes, and between those exist "Horizontal security consistency"

## Security service & Security service types

Security service is defined independently of the technical mechanisms used to deliver it. And it is derived exclusively from the contextual and conceptual layers above 

Examples:
* Entity auth service
* Stored data confidentiality service
* Monitoring service

Types:
* Application
** Primary (authentication, ACL, audit...)
** Secondary (confidentiality, integrity, authenticity)
* Middleware
** Explicit (via API)
** Implicit 

## Implications of static & Dynamic information, information flows & transactions on security service specification

Static information - such as master records, executable code, conf. information
* Does not move or change short term
* Services such as integrity protection or availability protection

Dynamic information - such as freeform messages, database queries, transaction information
* Services such as Authenticity of source or integrity protection

Protecting transactions require specific security services.

Primary services are self contained within a domain
Secondary security services operate between elements within a domain

## Position in the architecture Matrix of services, mechanisms, component & management activities

Within middleware, application, network, platform

## Principle of Security Service Value

Increases Service and performance potential, control and demand
Decreases risk and spare capacity

# Entity and trust framework

## SABSA concept of trust & trust models

For two entities to interacti requires trust. Trust is established through registration

All registered entities within a given domain trust one another within the domain policy

Transitive, or pass-through, trust happens via third party trust chain

## Roles of participants in SABSA trust model

-

## Process and rationale for decomposing complex two way trust

Complex two-way trust can be decomposed to different trust types

Such as business relationship can be decompised to
* Supply goods one way trust
* Pay for goods one way trust
* Card receipt, payment, timely information, authentication etc.

We trust because we build capacity to establish sufficient trust

## Chain of trust & trust hierarchies

RA can trust trutees of the trusted another RA

Superbrokers sell trust

# Inter-domain Security Associations

## Security associations concept & its objectives

Security association is a logical representation of the business requirements for trust and security
* Intra-domain (between entities in a single domain)
* Inter-domain (between entities in different domains)

Associations are achieved by deploying appropriate services

## Extended domain concept

Needed when one domain needs to exert control to antoher domain in order to manage its own risk. The dominant policy authority extends its domain into another and implants its policy into the 'territory' of another domain as special sub-domain.

Case SWIFT or Authentication server

## Importance of inter-domain modeling

All major operating systems have major security bugs

Knowledge of the vulnerability is retained in the architecture

# Service Sequencing

## Temporal considerations for security architecture

## Sequencing of security services

## Label logical relationships in authentication

* Claimant, verifier, exchange
Claim AI , Exchange AI , Verification AI

