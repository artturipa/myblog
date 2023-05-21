# Moar certificates

Next up, CAD exam. Below my notes.

## Application Development Overview

* Cloud-Based Application
* Why To Develop Custom Application
    * Replace old systems or processes
    * Extend value of servicenow
    * Extend service delivery and management across enterprise
    * Bring greater levels of automation and consolidation to enterprise services and their management
* What type of applications are good with for ServiceNow platform
    * It fits relational database
    * Extensive use of forms to interact with data
    * Reporting capability is required
    * Needs flows/workflows to manage processes
    * Can extend existing functionality with javascript
* What is not good fit for a ServiceNow application
    * Unstructured data
    * Need to propriatery libraries without APIs
    * Games or applications that require graphic engines
    * No process flow through application
* Differences scoped vs global applications
    * Scoped  
        * Scoped Sparate Namespace
        * Delegated Development
    * Global
        * Everything in Global
    * For Both
        * Source Control Integration
        * Publish to App Repository
* Build to global scope on these occasions:
    * Modifying global applications
    * Required resources not available from scopes
    * Extensive reliance on global resources 
* Global Scope applications can bypass scope protections, allowing them to:
    * Read records
    * Run API requests
    * Create Configuration records
* Scoped Development Process phases
    1. Analysis
    2. Design
    3. Development
    4. Test
    5. Deployment

**Update Sets**
Are essential for: 
* Customizing baseline applications 
* Customizing applications purchased from store.
Are useful for:
* Keeping track on why a change was made
* Exporting progress before instance clone
* Associating changes with SDLC artifacts (problems, stories, bugs, etc.)
* Deploying an application if the app repo is unavailable

## Application Analysis And Design

**Application Development Checklist**
* Define Process
    * Business Problem
    * Outcomes
    * Input(s)
    * Output(s)
    * User personas/stakeholders
    * Process steps
* Design and Build Data Model
    * Tables
    * Columns
    * Relationships
* Design and Create User Interface
    * Desktop/Tablet
* Apply Security
    * Roles
    * Access Control
* Automate
    * Flow Designer
    * Scheduled Script Execution
    * Email
* Integrate
    * SOAP/REST/CSV/Microsoft Excel
* Enhance User Interface
    * Service Catalog
* Test

**Delegated Development** 
* allows non-administrators to develop, deploy, and delete applications (with application-specific permissions and instance-specific user roles)
* Administrators can use Studio to manage development users and the application content they can access
* Is limited to scoped applications

**ServiceNow recommendations for Analysis and Design Phase**
* Develop private-scoped applications
* Follow delegated development practices
* Give every process its own scope
* Track development tasks

## Create Application and Modules

**Application Developer Tools**
* **Application Engine Studio (AES)** is the IDE
* **ServiceNow Studio** is IDE-like interface for application developers. 
* **Guided Application Creator (GAC)** is an intuitive development interface providing step-by-step process for application development

**Additional Application Development Tools** include:
* IntegrationHub
* Table Builder
* UI Builder
* Flow Designer
* Creator Workflows (tools that help lowcode developers automate processes: App Engine, Integrationhub, Manufacturing Connected Workforce)
* Process Automation Designer

**Steps in Guided Application Creator (GAC)**
* Application Configurations (Name, Description, Scope)
* User Roles (Existing/New)
* User Experience (Mobile/Classic)
* Tables (Existing/New)
* Field Inputs
* Table Configurations (Label, Auto-numbering, Manage access)
* Next Steps (Studio, Flow Designer, Set up another app)

**Source Control Recommendations**
* When creating a new branch, it should be **Tagged** in order to communicate the purpose
* **Stash** is a locally stored set of changes, and it allows moving changes between branches
* When working with Stashes, following steps are required:
    * Create a stash
    * Apply a stash to a branch
    * Manage possible conflicts (if there are more recent updates in the repository configurations)

**Studio Capabilities**
* Studio has
    * Navigation and tabbed environment
    * Code Search
    * Quick creation of scripts and files
    * Push (External Source Control Repository or Internal Application Repository)
    * Global application files management
* Studio does not have
    * Previous number check
    * Push to Update Set
    * Testing of the application
    * Script Intellectual Property protection
    * Ability to merge branches
    * Ability to add data
    * Form Layout

**Table Control** contains
* Extensibility
* Numbering
* Access

**Table Application Access** contains runtime access options
* Accessible From (scope)
* Caller Access (is based on scoped application restricted access plugin) tracks cross-scope application requests
    * Option --None--
    * Option: Caller Restriction
        * Manually approved
        * Tracked in the Restricted Caller Access table
    * Caller Tracking
        * Automatically approved
        * Tracked in the Restricted Caller Access table

**ServiceNow Recommendations - Applications and modules**
* Design Data Model before creating an application and tables in ServiceNow
* If possible, extend a ServiceNow table to gain functionality "for free"
* Link the application to a repository to manage the source code
* Comment every step of the application development process you can

## Application Forms
* Default view exists for new tables. When extending tables, default view is inherited.

* Components in form designer
    * Header, includes: 
        * Table
        * View
        * Actions (Undo & Save)
    * Field Navigator
    * Form Layout
        * Section & Fields (the button which gives more options is named "Handle")
* Annotation is a field type, which can be used to add information

**Form Based Client Scripts**
* onLoad()
* onSubmit()
* onChange()
    * Has parameters (control, oldValue, newValue, isLoading, isTemplate)

**Client script APIs include**
* g_user
* g_form

**Client scripts vs UI Policies**
* UI Policies execute BEFORE client scripts
* UI Policies provide better performance than client scripts
* Client scripts have access to fields prior value, UI Policies do not
* Client scripts can execute after list field value change
* Client scripts can execute on form save/submit/update

**Publishing and Committing to git**
* Publishing an application __automatically__ commits local changes to git repository, if application has one
* If all the changes are not ready for commit, work in progress configurations should be stashed

**Uninstall or Rollback an Application**
* In the application record, one can roll back to previous version of the application 
* Uninstall is also possible from the application record

**ServiceNow recommendations**
* Create as few new fields as possible
* Design forms and lists for the best user experience
* Use scripts to enhance the user experience
* Test on tablets and smartphones to verify usability
* Use a repository to move applications between instances

## Control Access

**Access Control Rule Evaluation**
1. Match the object against table ACL rules (most specific to most general)
    1. incident
    2. task
    3. *
2. Match the object against field ACL rules (most specific to most general)
    1. incident.number
    2. task.number
    3. *.number
    4. incident.*
    5. task.*
    6. *.*

**Evaluation order of single ACL rule**
    1. roles
    2. conditions
    3. script

**ServiceNow Recommendations**
* Plan security settings early in the application development process
* Create user and admin roles for application modules
* Test all new application features against security settings
* Control access with roles for easy maintenance
* For best performance and security, avoid using client-side API methods such as g_suer.hasRole() to control access
* Test applications by impersonating different users
* Use Application Access to specify which application artifacts are available to other scopes

## Automate Work

**Flow Designer**
* Flow Trigger types are
    * Application (such as metric base or service catalog, integrationhub allows adding to Application triggers)
    * Record
    * Schedule
* Testing the flow does not provide rollback
* Use Flow Designer over workflow if
    * Running Kingston or newere
    * Trigger is CRUD table operation or schedule
    * Actions/Steps are available in Flow Designer
    * Logic includes if/then branching or linear flow

**Spoke** is a Scoped Application containing Flow Designer content for an application or record type

**Application Properties** are useful for:
* Setting values from an application properties page
* Single location for all application properties
* Retrieving values to use in scripts

**Events** are recorded in event log, and they can trigger email notifications and script actions
* ServiceNow can only respond to Events that are registered to **event registry**
* Events go to default queue if no queue is specified
* Event processing duration is shown in milliseconds

About **Script Includes:**
* Prototype function contains logic all objects instantiated from the class will have access to.
* The initialize function is automatically invoked when the object is instantiated

**ServiceNow recommendations**
* Automate as many process steps as possible to reduce human error
* Virtualize processes with Flow Designer or Workflow
* Use application properties to manage configurable application settings
* Use Scheduled Script Executions with events and email to execute script on a time basis
* Utilize Script Includes 

## Import and Integrate

* Integration Interfaces
    * Authentication
    * Integration Hub
    * File Import
    * File Export
    * URL Access
    * Platform Web Services
    * Scripted Web Services
    * Database
    * Email

**Import Data via Guided App Creator:**
* Create Table from Upload Spreadsheet
* Upload XLSX
* Define Schema
* Create Table

**REST Message** records are:
* Used to develop, prototype, and save outbound REST messages
* Reusable in Business Rules, Email Notifications, and other server-side scripts

**Web Service** is a web-based method allowing applications to connect to other software applications over a network

**ServiceNow recommendations**
* Always clean up data before importing into ServiceNow
* Understand the format/structure/contents of the data before importing
* When importing, determine how to coalesce
* Study and understand what a web services expects to receive and the format of the response
* Test REST Message Functions
* Do NOT practice with the REST API Explorer on a production instance

## Testing

**Software Testing Lifecycle**
1. Requirement Analysis
2. Test Planning
3. Test Case Development
4. Environment Setup
5. Test Execution
6. Test Cycle Closure

**SN Test Management** is for manual tests, and it manages all phases of the testing process
* Test Repository contains tests, test cases and test suites
* Test execution contains Test environments and Test plans

## Specifics

* It is recommended to create a System Property Category and a Module for set of (ordered) properties
* Applications can be published to repository or to a store
* glide.appcreator.company.code property (maint only) has to have same value for instances sharing apps in application repository
* In studio, Icon Status Bar (bottom) shows whether the application is connected to Source Control 
* All applications do have scope, global or private
* All tables have 6 default fields
    * Updated + Updated by
    * Created + Created by
    * sys_id
    * Updates (number of updates for the record)
* Display Business Rules can be used to pass string values to client via g_scratchpad,
* Table.None ACL is needed in order to view table's list or form
* Application Protection Policies only apply if application is published to ServiceNow Store
* In Scheduled Script, anything that has been a variable in the __condition__ field, are available to the script itself
* Only Notifications with the highest weight for the same record and recipients are sent (+ notifications with 0 weight)
* Users have Notification-field, which defines whether the user is receiving notifications
* Script Actions respond to events, and have two objects they can access:
    * Event Object containing the parameters
    * Current = object passed in from gs.eventQueue()
* REST Message Variable Substitutions are used when testing a HTTP Method
* Table record has Related Link UI Action "Add to Service Catalog", which is a shortcut to create record prodcuer for the table. 
* The platform is a __contextual__ development environment
* **Runtime Access Tracking** can be used to manage script access to resources from other applications. This is known as cross-scope access, as the records are in different scopes. Settings are:
    * **None** - No authorization required for application scripts to access resources as long as the other application allows it. No record is being created in the Application Cross-Scope Access -table.
    * **Tracking** - Allows application scripts to access resources from other applications. A record for the access is automatically inserted in the Application Cross-Scope Access table, with __Status__ value of __Allowed__.
    * **Enforcing** - Allows application scripts to access resources only after administrator has authorized the access. The cross-scope access record is automatically created with __Status__ as __Requested__.
* Script API and Web Services can be refered as **Runtime access points**
* Application Creation Options
    * Start from scratch 
        * Empty Application, for example if application just has one configuration record
    * Create a custom application 
        * For applications that include UIs and Data elements
    * Start from a template
    * Start from an existing service 
        * Converts existing service to an application if **Service Creator** is active
    * Start from global
        * In order to do it, property **glide.app.creator.global** needs to be __true__
* Update Sets track customizations to tables that have **update_synch** dictionary attribute
* **Special Handlers** are used to track changes that affect multiple tables. Following changes are tracked with special handlers
    * Workflows
    * Form sections
    * Lists
    * Related lists
    * Choice lists
    * System dictionary entries
    * Field labels
* Application scope can have only one **default update set**
* $m.do gives the mobile version of the application
* **Embedded list** is a form element, which allows editing related lists without having to navigate away from the form. Changes are saved when the form is saved
* **Response time indicator** is a form element, which appears at the bottom of some forms to indicate the processing time require to display the form
* **Override Application Menu roles** option allows granting module level access to role that is not allowed to view the application.
* **Document feed** is a live feed group that is associated with a record. Functionality is used when one follows a record.
* **Import Data Sources**
    * CSV
    * JDBC
    * FTP
    * HTTP
    * XML
* Unpublished workflow won't be captured in a update set
* Event **system.upgraded** verifies system upgrade
* Types of UI Actions
    * Form buttons
    * Form context menu items
    * Form links
    * List Buttons
    * List context menu ites
    * List Choices (at the bottom of a list)

### Team Development
* **Team Development** supports parallel development on multiple sub-production instances. Also following features are provided:
    * Branching operations, including pushing and pulling record versions between instances
    * The ability to compare a development instance to other development instances
    * A central dashboard for all Team Development activities
* **Local Changes** table tracks which customized records have current versions on the development instance but not on the parent instance
* Team Development uses **Version Records** to manage versions (not Git)
* **Team Development credentials** give access to administrate remote instances, push changes to parent instance and use __Code Review Requests__ -module
* User with admin or **teamdev_user** role has access to register a remote instance, and do other team development actions.
* User with admin or **teamdev_code_reviewer** role has access to Code Review Requests module.
* **Exclusion Policies** allow developers to prevent pushes or pulls to particualr instance in the development hierarchy.
* Team Development Administrators can require that pushes undergo **Code Review** before acceptance
* When **Code Review** is enabled, pushes to parent instance trigger the Code Review __workflow__
* Code Review -workflow sends notifications to __reviewers group__ when push __requires a code review__ or when __a user cancels a push__.

    

## Actually useful

* Adding links to notifications:
    * ${URI}: link to open the record, with label LINK
    * ${URI_REF}: link to open the record, with label Display Name
    * ${<reference_field_name>.URI}: link to open a related record, with label LINK
    * ${<reference_field_name>.URI_REF}: link to open a related record, with label Display Name
* ctrl-spacebar provides list of classes in a script
* Pass script into Email notification via <mail_script> </mail_script>, there print values with template.print() -method. When saved, system will ask to save it as a email notification script -record
* Indicators when editing Access Controls
    * Red text: An Access Control that was activated or deactivated
    * Blue text: An Access Control that was modified
    * Green text: An Access Control that is added or has become active
    * Masked: An Access Control that was effective until you made a change
    * Unmasked: An Access Control that was made effective when you made a change
* ACL debug indicators:
    * Green: Access granted
    * Red: Access denied
    * Blue: Not re-evaluated, already in cache
    * Gray: Not evaluated, part of the rule has already denied access
    * Checkmark: Passed
    * X: Failed