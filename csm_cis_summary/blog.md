# Here again !

Long time no blogging! The reason being lack of time. I am currently solution architect in three simultaneous implementation project, so days tend to be quite hectic.

Not to make my life too easy, I decided to reserve a slot for CSM CIS exam. The exam is in two weeks so I time to start prepping. CIS exams often have questions about specific configurations, such as names of flows or plugins, and hence some studying is needed.

Below are key notes that I recapped for CIS exam.

# CSM recap

## Key Definitions

**CSM Application scope** includes Cases, Accounts, Contacts, Service Contracts and Entitlements, Assets and product models, Service Portals and/or CMS, Knowledge base and reporting

**ServiceNow's industry solutions are built on top of CSM**. Industry solutions include Telco, Financial Services, Healthcare and Public Sector

**Service-aware install base** allows organizations to:
* Model complex products and services with components
* Quickly identify products sold and installed
* Track related operational services and configuration items that affect service health
* View products not yet purchased or deployed by customers

**Service-aware install base entities** include:
* Product Model
* Install Base Item
* Installed product

**Product** is a good or a Service that a company sells to, and supports for their customers.

**Models** are specific versions of items in the environment. Model record allows maintaining information about the specific model ensuring data consistency.

**Model Categories** are part of Product Catalog and they associate CI classes with Asset classes. Model category configuration specifies whether an asset is created from a CI. Model Categories are set to Product Models.

**Product Portfolio** is comprised of all the products an organization has to offer.

**Asset** [alm_asset] is a specific product instance which is purchased / subscribed by a customer. Asset Management is activated when CSM is installed. Five different asset classes are:
* Hardware Assets [alm_hardware]
* Software License Assets [alm_license]
* Consumables [alm_consumable]
* Enterprise Software Assets [alm_application_software]
* Facility Assets [alm_facility]

**Contact** - Member of an external company. Customer user in B2B -model, contact can be related to only one account. They are not able to login into the system unless an user record is associated with them, user record is created automatically. Customer Service Managers and System Administrators can create contacts.

**Customer Service Agents** - Users of the organisation who provide customer service and work with cases. Agents are organised on groups and skilled on specific products.

**Service Management** connects customer service to the rest of the organization, making collaboration about customer issues with other departments easier.

**Tier 3 support agent**  is a person with compherensive knowledge of a particular area

**Customer Service Supervisors and Managers** oversees operations in customer service including service delivery, personel management and escalations

**Business Managers and Executives** is a person responsible for the overall customer service organization

**Business Contributors** sales managers, account managers, etc.

**Core Master Data** is often referenced by the case, includes accounts, contacts, users, products, assets, locations and groups

**Account** stores the Account’s information, such as name, account number, primary contact, phone number, address, and company website address. 
* Only Customer Service Manager and System Administrators can create accounts.
* Account can have multiple addresses but only one primary address. Primary address is included in **Addresses** related list with Primary set as **true**

**Account Relationship Types** - System Administrator can create additional relationship types. Default relationships are:
* Partner-to-account
* Account-to-account

**Account Hierarchy** allows modeling legal entity structure and their relationships. A relationship can be created by System Administrator or Customer Service Manager. Customer admins are able to view cases, assets and users for all the subsidiaries under their own account.

**Contact Relationships** enable admins and/or managers to add contacts under multiple accounts. Hence, same contact can be associated with multiple accounts.  

**Account Path** - Is automatically generated code which tells the hierarchy of a given account. Max depth is 63 levels.

**Post Case Review**
After resolution of a case, one can trigger post case review to capture details about resolved case, affected assets, root cause, resolution and preventive measures.

**Installed Products** is a class, which connects **Install base items** to **Sold products**

**Agent Whisper** allows users with __awa_manager__-role to join chat conversations and chat privately with the customer service agent.

**Parent/child synchronization** allows one to control the child case behaviour through the parent record. Admins can control which fields cascade. It only goes one level deep and closed/resolved cases are not synced.

**Assignment Workbench** enables customer service managers to assign tasks to agents. Workbench uses configurable criteria such as skills and availability to evaluate agents in a selected group to provide overall ranking. 

**Advanced Work Assignemnt** removes manual routing of work and prevents cherry picking tasks.

**Self Registration** allows contacts to self register via portal by submitting registration request. 

**Unified portals** allow easy configuration of multiple portals with unified look & feel and a unified navigation menu structure.

**Benefits of Proactive Customer Service Operations**
1. Faster resolution time
2. Lower call volume
3. Improved customer experience

**Three Components of Proactive Service operations:**
1. Service monitoring (detect issues)
2. Service-aware install base (identify impacts)
3. Proactive case (Notify customers)

**Three types of outages:**
1. Unplanned outage
2. Planned outage
3. Degradation

**Social Profiles** can be created for an accont, contact or consumer. And they can be created by Customer Service Managers. Social profiles can be associated to Account, Contact and Consumer

**Entitlement** - Defines the support customer receives and supported channels for the customer. Is measured by cases and/or hours. Entitlements can be made of products, assets and/or contracts (cascades to assets covered).

**OOB integrations to other modules**
* ITSM
* PPM 
* FSM
* ITOM

**Key capabilities of PPM Integration**
1. Data model changes allows creating project accounts
2. Creating cases against projects
3. UI and Business Logic
4. Portal changes to view status and project assignments

**CSM Portals**
* Customer support (/csm)
* Consumer Service (/csp)
* Community (/community)
* Knowledge management (/kb)

**Baseline Catalogs**
* Consumer
* Customer
* Technical
* Service
* Field Service

**Data analysis use cases in CSM**
* Anticipate trends
* Prioritize Resources
* Deliver automation and self service
* Drive continual improvement
* Align customer service

**Response Template** are reusable messages that can be copied to a case or task from.

**Agent Affinity** is AN AWA feature that allows assigning agent tasks based on following details:
* Historical tasks
* Related Tasks
* Account team
* Responsibility

**Case Action Summaries** provide updates to customers and internal stakeholders while case is in progress. Summaries are closed when the case is closed.

**Skill Based Routing**

**Order**

**Publication**

**Contracts** - Can be associated to sold products.

**Real-time SLAs**

**Service Contract** contracts group together SLAs that relate to a single vendor or customer, as well as the CIs, locations, groups, users, and child contracts that are related to the contract.

**Customer Self Service portal** - Allows customers to view Assets, Orders and Publications

**Openframe** Provides a communication frame for agents for customer calls. It allows CTI capability with multiple telephony service providers.

**Resolution Shaper** - Timeline that is shown in case record. There blue circle represents state change and line represents any other activity than state change. Customers' updates are below, agents updates are above.


## Default Settings
* Flow of states in case is new, open, awaiting info, resolved, closed
* Agents can manually close a case, if resolution code and -notes are filled.
* From case to knowledge article following fields are copied: Short Description, Cause, Close Notes (-> Resolution) 
* Special handling notes can be created via "Form Link" -button or via Special handling notes module.
* Assignment Workbench default configuration uses **Recommendation for Case Assignment** matching rule, which uses three of the four default matching criteria:
    * Availability Today
    * Matching Skills
    * Assigned Cases
    * Not used: Last assigned
* Customer Service Agents are the ones who manage case escalations
* Account escalation manager manages account escalations
* To use Time Recording, following steps need to be taken:
    1. Enable plugin
    2. Give managers the _timecard_admin_ role to approve time sheets
    3. Give agents the _timecard_user_ role to fill in time cards and time sheets
* Recipient lists can be created by:
    1. By importing account, consumer, or internal user information
    2. By importing contact information
    3. By using a script
* Resolved cases or cancelled cases or cases with a parent can't be major case candidates
* When major case is being made a child of a normal case, the major case becomes a normal case
* To extend functionalities of major cases, extention points are being used
* All four CSM portals support unified theme
* Users that can create a case from a question
    1. Customer Service Agents
    2. Consumer Service Agents
    3. Customer Service Managers
    4. People with the proxy_case_creator role
* Channels available on the Customer Support Portal are Web and Email
* Partner admins have access to Partner- and Customer Accounts.
* When consumer self registers, a record is inserted in *Consumers* and *Consumer users* -tables.
* Account relationships can be created by admin and customer service manager roles.
* Public Knowledge includes _Rate_, _Flag_ and _Helpful_

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

**Deactivate Special Handling Notes [Scheduled Job]** runs daily at midnight to expire special handling notes that have enabled their expiration dates.

**Flows for the email channel**
* Create case from email
* Update case from email

**Auto close resolved cases [flow]:** 
* After 5 days a reminder is sent that solution acceptance is pending
* After 10 days case is closed and a notification is sent about the closure

**Customer Survey is sent** when case is closed.

**Business rules associated with Self Registration registration code**
* "Display request message" - Shows info message to user
* "Display rule" - Shows message to remind user to enter a correct registration code


### Tables

**CSM Essentials**
* Account [customer_account] - extends [core_company]
* Contact [customer_contact]
* Consumer [csm_consumer], if self-registered then stored in csm_consumer_user
* Order case [csm_order_case] - extends Case
* Service Contract [ast_service] - extends the table *Contract*


**Assignment Workbench**
* Matching Criteria [matching_dimension] - Stores the matching criteria that can be used to create a configuration for the assignment workbench.
* Select Criteria [matching_dimension_for_assignment] - Stores the matching criteria for an assignment workbench configuration matching rules.
* Matching Rule [matching_rule] - Stores matching rules, including the matching rules that configurations for the assignment workbench.

### Plugins

**CSM essentials**
* Customer Service Management for Orders [com.snc.csm.order]
* Customer Service Portal [com.glide.service-portal.customer-portal]
* Targeted Communications [com.sn_publications]
* Customer Service [com.sn_customerservice]
* Customer Service Install Base Management [com.snc.install_base] / is needed for Service-aware install base features
* Performance Analytics - Content Pack - Customer Service [com.snc.pa.customer_service]
* CTI Softphone [com.snc.cti] / Enables customer service and Twilio using notify

**CSM integration to other modules**
* Customer Service with Field Service Management plugin (com.snc.csm_fsm_integration)
* Integration with Financial Management
* Customer Service integration with Service Management [com.sn_cs_sm]
* Customer Service with Request Management [com.sn_cs_sm_request]
* Integration to Problem Management functionalities
    * Problem Management Best Practice - Madrid [com.snc.best_practice.problem.madrid]
    * Problem Management Best Practice - Madrid - State Model [com.snc.best_practice.problem.madrid.state_model]
* Customer Service Case Action Status [com.snc.csm_action_status] - Provides actionable case flows.

**Knowledge Management**
* For translation: I18N:Knowledge Management Internationalization v2 plugin [com.glideapp.knowledge.i18n2]
* For versioning: Knowledge Management Advanced

**Internationalization**
* l18N:Knowledge Management Internationalization V2


### Roles

**CSM Primary Roles**

B2B & B2C
* sn_customerservice_manager
* sn_customerservice_agent

B2C
* sn_customerservice.consumer_agent
* sn_customerservice.consumer

B2B Customer
* sn_customerservice.customer
* sn_customerservice.customer_admin
* sn_customerservice.customer_case_manager

B2B Partner
* sn_customerservice.partner
* sn_customerservice.partner_admin

*CSM Base Roles*
* sn_esm_agent
* sn_esm_admin
* sn_esm_partner
* sn_esm_partner_admin
* sn_esm_user
* sn_esm_user_admin

_Customer Service Agents_
* sn_customerservice_agent
* sn_customerservice_consumer_agent

_Customer Service Manager_ - Customer service agent with the additional responsibility for managing agents or agent groups and overriding agent actions.	
* sn_customerservice_manager

**Additional Roles**
* Case contributor editor [sn_customerservice.case_contributor_editor] - This role provides limited write access to the fields on the Case form.
It provides limited write access to those cases for which the user already has read access provided by another role.

* Case contributor viewer
[sn_customerservice.case_contributor_viewer] - This role provides read-only access to all of the tables associated with a case. With this role, a user can view the information in the related lists for a case if other conditions are satisfied in the case.

* Case task agent [sn_customerservice.case_task_agent] - This role provides access to case tasks and related case information

* Case task viewer [sn_customerservice.case_task_viewer] - This role provides read-only access to all case task records.

* Case viewer [sn_customerservice.case_viewer] - This role provides read-only access to all cases.

* Contact manager
[sn_customerservice.contact_manager] - User who can manage contacts.

* Customer project manager
[sn_customerservice.projectmanager] - A user who creates and manages projects for customer accounts. Comes with customer project managemen plugin (com.snc.csm_ppm)

* Customer project stakeholder [sn_customerservice.projectstakeholder] - A user who is responsible for activities that require viewing customer project details and project tasks.

* Data viewer [sn_customerservice.customer_data_viewer] - User with read-only access to customer data entities 

* De-escalation requester
[sn_customerservice.deescalation_requester] - User who can deescalate a case or account when the cause of the escalation is resolved.

* Escalation requester
(sn_customerservice.escalation_requester) - User who can request an escalation for a case or account.	

* Proxy case creator
[sn_customerservice.proxy_case_creator] - Users with the proxy case creator role can create customer service cases directly from community questions created by contacts or consumers

* Proxy contact
[sn_customerservice.proxy_contact] - Role that enables employees to create cases for customer accounts and contacts. Employees can also be proxy case contacts on behalf of customers. Assign this role to employees in your company who are not fulfillers or do not have other CSM-specific roles.

* Workspace user
[sn_customerservice.csm_workspace_user] - Provides access to CSM workspace

### Roles installed with the Customer Service Base Entities plugin
* Service management agent [sn_esm_agent]
* Service management partner [sn_esm_partner]
* Service management user admin [sn_esm_user_admin]
* Service management admin [sn_esm_admin]
* Service management user [sn_esm_user]
* Service management partner admin [sn_esm_partner_admin]
* Role for REST APIs related to CSM web services [csm_ws_integration]

**Assignment workbench**
* Assignment workbench [assignment_workbench] - Provides access to the assignment workbench for customer service agents and consumer service agents.
    * Contains Skill user[skill_user]

### Properties

**Assignment workbench**
* *assignment_workbench.find.agents.title* - Title for the macro button.
    * Default Value = "Find Agents"
* *assignment_workbench.new.window* - When enabled, opens the assignment workbench in a new window.
    * Default Value = false
* *assignment_workbench_no_of_agents* - Number of agents per page. (To get better performance, do not use more than 50 agents per page.)
    * Default Value = 30 

**Special handling notes**
* Maximum number of notes displayed in the pop-up
    * Default value = 20
* Display special handling notes only once per session
    * Default value = yes

**Knowledge management**
* **glide.knowman.search.default_language** allows forcing a default language for knowledge articles.
* _"Enable access control of Knowledge Bases based on product entitlements"_ -property exists.

**CMDB**
* **sn_customerservice.use_asset_contact_relationship** can be used to restrict contact access to assets. When enabled, only assets where the user is a contact are shown.

### Specifics

**Types of CSM cases** are Product and Order

**Knowledge Product Entitlement** restricts access to Knowledge bases and articles based on products owned by the customer or consumer.

**Updating consumer record** Following roles can update: sn_customerservice_manager, sn_customerservice.consumer_agent, (admin). Default agent can not.

**Generic entitlement** is a product entitlement without a company.

**External customers and/or partners can view and approve requests and change requests**. They can also see ITSM tickets that relate to a case they have access to.

**CSM Guided Setup includes**
* Percentage of activities completed
* Controls to start, skip, and mark tasks as complete
* Plugin management
* Links between CSM and other applications (including ITSM, ITOM, SPM, KM, PPM)
* A link to Community and FSM Guided Setup

**Entitlement counter** calculates whenever a case with an associated entitlement is closed. It only runs if the _per unit_ field is enabled.

**Cases can be created from questions on portals by:**
* Service Agents
* Customer Service Managers
* Users with the sn_customerservice.proxy_case_creator

**Chat quick actions:**
* /tq - transfer to queue
* /ta - transfer to agent
* /r - use response template

**Account address types:**
* Primary (only one is allowed)
* Billing
* Shipping
* Custom

#### Communities

**Communities** functionality is only available via CSM and it is not automatically activated with CSM plugin.

**Forums in communities** group users together to discuss items of mutual interest. These items are _Topics_.

**Content types in communities** are:
* Q&A
* Blogs
* Videos
* Comments

**Forum content can be viewed from:** 
* Content Feed and Activity Feed on the _Home page_ or on the _user profile_ specific to that user.
* Content Feed specific to a Forum on the Forum page
* Content Feed specific to a Topic on the Topic page

**Supported content feedback** includes:
* Comment (Blogs and Videos)
* Up-votes (Questions)
* Helpful (Answers, Blogs and Videos)
* Mark as Correct (Answers)

**In another user profile following details are included:**
* Posts and Activities
* Contributions
* Correct Answers
* Forums Subscribed

**Flagging a comment** creates a moderation task.

#### Other

**Unified portal header** includes
* Self Registration
* Typeahead search
* Profile
* Chat
* Login/Logout
* Customer Title
* Notifications

**Branding editor quick setup tab** allows customization of:
* Theme colors
* Text colors
* Portal title 

**Associating Partner with an Account** causes partner to inherit all child accounts.

**Partner Account** - Accounts can be customer, partner or customer&partner accounts. Partner accounts support customer accounts, and they can report and manage cases on behalf of customer accounts. 

**Third party** is an organization that has been contracted to sell products and services they have **purchased** from another organization. 

**Third party owns the relationship with a customer**. A partner __does not own the relationship__ with a customer, the relationship is owned by the organization they are partnering.

**Partner contacts** can be associated with assets.

**In case of multiple Openframe configurations**, the one with lowest order is assigned to user.

**Email addresses for CSM** are configured in _Channel configuration_ [comm_channel_config]

**Chat queues activated via CSM Plugin** are Customer Service and Customer Service Support

**Cases are created _manually_ from social channels** by agents, and channel is set to _Social_.

**_Standard_ Special Handling Note** relates to specific record. Another type is conditional.

**Matching rules run** before assignment rules and it runs only if task is not already assigned to another user or group.

**Unique email address is required** in self registration.

**Results of a Knowledge base search include:**
* Matching articles
* Matching Q&A
* Matching Service catalog
* Matching Case

**Asset Contact** - Administrators can add a primary contact to an asset. When added, the primary contact is also added as an Asset Contact to the corresponding related list by __Add Primary Contact__ -business rule.

* All WebDAV -compliant knowledge content can be improved from external knowledge sources.
* Following activities are available offline in FSM mobile application:
    1. Execute assigned tasks
    2. Close completed work orders
    3. Manage assets
* If a company wants to support Twitter, Twitter profile details should be stored in *Social profile*

