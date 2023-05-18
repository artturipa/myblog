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
* ctrl-spacebar provides list of classes in a script
* Display Business Rules can be used to pass string values to client via g_scratchpad,
* Table.None ACL is needed in order to view table's list or form
* Application Protection Policies only apply if application is published to ServiceNow Store
* In Scheduled Script, anything that has been a variable in the __condition__ field, are available to the script itself
* Only Notifications with the highest weight for the same record and recipients are sent (+ notifications with 0 weight)
* Users have Notification-field, which defines whether the user is receiving notifications
* Adding links to notifications:
    * ${URI}: link to open the record, with label LINK
    * ${URI_REF}: link to open the record, with label Display Name
    * ${<reference_field_name>.URI}: link to open a related record, with label LINK
    * ${<reference_field_name>.URI_REF}: link to open a related record, with label Display Name
* Script Actions respond to events, and have two objects they can access:
    * Event Object containing the parameters
    * Current = object passed in from gs.eventQueue()