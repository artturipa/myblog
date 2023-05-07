# Here again !

Long time no blogging! The reason being lack of time. I am currently solution architect in three simultaneous implementation project, so days tend to be quite hectic.

Not to make my life too easy, I decided to reserve a slot for CSM CIS exam. The exam is in two weeks so I time to start prepping. CIS exams often have questions about specific configurations, such as names of flows or plugins, and hence some studying is needed.

Below are key notes that I recapped for CIS exam.

# CSM recap

## Key Definitions

*CSM Application scope* includes Cases, Accounts, Contacts, Service Contracts and Entitlements, Assets and product models, Service Portals and/or CMS, Knowledge base and reporting

*Customer Support Agent* - Users of the organisation who provide customer service and work with cases. Agents are organised on groups and skilled on specific products.

*Tier 3 support agent* - is a person with compherensive knowledge of a particular area

*Customer Support Agent Manager* - Oversees operations in customer service including service delivery, personel management and escalations

*Customer Service Executive* - Is a person responsible for the overall customer service organization

*Core Master Data* - Is often referenced by the case, includes accounts, contacts, users, products, assets, locations and groups

*Account Path* - Is automatically generated code which, tells the hierarchy of a given account. Max depth is 63 levels.

*Post Case Review*
After resolution of a case, one can trigger post case review to capture details about resolved case, affected assets, root cause, resolution and preventive measures

*Installed Products*
Class which connects *Install base items* to *Sold products*

*Agent Whisper* 
Allows users with *awa_manager*-role to join chat conversations and chat privately with the customer service agent.

*Parent/child synchronization* 
Allows one to control the child case behaviour through the parent record. Admins can control which fields cascade. It only goes one level deep and closed/resolved cases are not synced.

*Assignment Workbench* 
enables customer service managers to assign tasks to agents. Workbench uses configurable criteria such as skills and availability to evaluate agents in a selected group to provide overall ranking. 

*Advanced Work Assignemnt*
Removes manual routing of work and prevents cherry picking tasks

*Support Model* tells how support is provided. Two options are:
* Entitlement only
* Entitlement plus service contracts

*Time Recording*

*Three Components of Proactive Service operations:*
1. Service monitoring (detect issues)
2. Service-aware install base (identify impacts)
3. Proactive case (Notify customers)

*Three types of outages:*
1. Unplanned outage
2. Planned outage
3. Degradation

*Benefits of Proactive Customer Service Operations*
1. Faster resolution time
2. Lower call volume
3. Improved customer experience

*Key capabilities of PPM Integration*
1. Data model changes allows creating project accounts
2. Creating cases against projects
3. UI and Business Logic
4. Portal changes to view status and project assignments

*OOB integrations to other modules*
* ITSM
* PPM 
* FSM
* ITOM

*CSM Portals*
* Customer support (/csm)
* Consumer Service (/csp)
* Community (/community)
* Knowledge management (/kb)

*Baseline Catalogs*
* Consumer
* Customer
* Technical
* Service
* Field Service

*Data analysis use cases in CSM*
* Anticipate trends
* Prioritize Resources
* Deliver automation and self service
* Drive continual improvement
* Align customer service

*Response Template* are reusable messages that can be copied to a case or task from.

*Agent Affinity* is AWA feature that allows assigning agent tasks based on following details:
* Historical tasks
* Related Tasks
* Account team
* Responsibility

*Real-time SLAs*

*Service Contracts*

*Skill Based Routing*

*Order*

*Publication*

*Service Contract* contracts group together SLAs that relate to a single vendor or customer, as well as the CIs, locations, groups, users, and child contracts that are related to the contract.

*Customer Self Service portal* - Allows customers to view Assets, Orders and Publications

*Openframe* - Allows CTI capability with multiple telephony service providers.





## Default Settings

* *Auto close resolved cases* -flow 
    * After 5 days a reminder is sent that solution acceptance is pending
    * After 10 days case is closed and a notification is sent about the closure
* Agents can manually close a case, if resolution code and -notes are filled.
* From case to knowledge article following fields are copies: Short Description, Cause, Close Notes (-> Resolution) 
* Special handling notes can be created via "Form Link" -button or via Special handling notes module.
* Assignment Workbench default configuration uses *Recommendation for Case Assignment* matchin rule, which uses three of the four default matching criteria:
    * Availability Today
    * Matching Skills
    * Assigned Cases
* Customer Service Agents are the ones who manage case escalations
* Account escalation manager manages account escalations
* To use Time Recording, following steps need to be taken:
    1. Enable plugin
    2. Give managers the timecard_admin role to approve time sheets
    3. Give agents the timecard_user role to fill in time cards and time sheets
* Recipient lists can be created by:
    1. By importing account, consumer, or internal user information
    2. By importing contact information
    3. By using a script
* Resolved or cancelled or cases with a parent can't be major case candidates
* When major case is being made a child of a normal case, the major case becomes a normal case
* To extend functionalities of major cases, extention points are being used
* All four CSM portals support unified theme
* Users that can create a case from a question
    1. Customer Service Agents
    2. Consumer Service Agents
    3. Customer Service Managers
    4. People with the proxy_case_creator role
* All WebDAV -compliant knowledge content can be improved from external knowledge sources.
* Following activities are available offline in FSM mobile application:
    1. Execute assigned tasks
    2. Close completed work orders
    3. Manage assets
* If a company wants to support Twitter, Twitter profile details should be stored in *Social profile*
* Channels available on the Customer Support Portal are Web and Email?????
* Partner admins have access to Partner- and Customer Accounts.
* Customer admin and Partner admin are the only two external roles
* When consumer self registers, a record is inserted in *Consumers* and *Consumer users* -tables.


## Guidance

* Integration process should cover:
    1. Integraiton approach (batch, real time, hybrid)
    2. Triggering event
    3. Filters
    4. Fields
    5. How users will get notified in case of failure

* Types of CSM integraitons:
    1. Data Integrations
    2. Case History
    3. Knowledge Article
    4. Softphone integration
    5. Master data from CSM
    6. Enterprise Resource Planning (ERP)
    7. SDLC
    8. Computer Telephony Interface
    9. Store and partner integrations

* Implementation considerations in Data migration
    1. Define legacy data conversions
    2. Review legacy data to remove obsolete data
    3. Tag imported data for future identification purpose
    4. Focus on high value content, plan for appropriate resources time and efforts

* Common types of data in data migration
    * Core master data
    * Cases
    * Attachments for cases and knowledge records




## Configurations

### Tables

*Assignment Workbench*
* Matching Criteria [matching_dimension] - Stores the matching criteria that can be used to create a configuration for the assignment workbench.*
* Select Criteria [matching_dimension_for_assignment] - Stores the matching criteria for an assignment workbench configuration matching rules.
* Matching Rule [matching_rule] - Stores matching rules, including the matching rules that configurations for the assignment workbench.
* Service Contract [ast_service] - extends the table *Contract*
* 

### Plugins
* Customer Service Management for Orders [com.snc.csm.order]
* Customer Service Portal [com.glide.service-portal.customer-portal]
* Targeted Communications [com.sn_publications]
* Customer Service [com.sn_customerservice]
* Performance Analytics - Content Pack - Customer Service [com.snc.pa.customer_service]
* CTI Softphone [com.snc.cti] / Enables customer service and Twilio using notify
* 


### Roles

*Assignment workbench* 
* Assignment workbench [assignment_workbench] - Provides access to the assignment workbench for customer service agents and consumer service agents.
    * Contains Skill user[skill_user]

### Properties

*Assignment workbench*
* *assignment_workbench.find.agents.title* - Title for the macro button.
    * Default Value = "Find Agents"
* *assignment_workbench.new.window* - When enabled, opens the assignment workbench in a new window.
    * Default Value = false
* *assignment_workbench_no_of_agents* - Number of agents per page. (To get better performance, do not use more than 50 agents per page.)
    * Default Value = 30 



https://quizlet.com/ca/588535526/servicenow-csm-fundamentals-flash-cards/
72 menossa
https://quizlet.com/271242864/servicenow-cis-csm-customer-service-management-flash-cards/52 menossa 
