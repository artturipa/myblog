# Moar certificates

Next up, SAM exam. Below my notes.

## Capability Blueprint

Is derived from the ISO 19770-1 Software Asset Management process standard. 

Four tiers:
1. **Trustworthy data** - Know what you have so that it can be managed
2. **Practical Management** - Improvement management controls and drive immediate benefits
3. **Operational Integration** -  Improve the efficient and effectiveness through integration with other areas (ITSM)
4. **Strategic Conformance** - Achieve best in class
    * Aims to manage change within software environment to achieve and support positive business outcomes

## Required Data

**Entitlements** (identify how many rights are purchased for using the software in your environment)
* License Metrics
* Purchase Rights
* Active rights
* Allocations Available

**Allocations**
* Per Device
* Per User

**Software Model**
* Publisher
* Product
* Suite Information
* Entitlements
* End of Life

**Foundation Data**
* Users
* Departments
* Cost centers
* Locations
* Vendors

## Terminology 

**Discovery Pattern** - Used to discover software installations
**Software Discovery Model** - Software model that is automatically created during discovery or import process.
**Software Discovery Map** - Set of conditions that determine which software discovery
**Pattern normalization rule** - Normalizes specific software products within an environment based on a common pattern
**Normalization status** - Identifies level of normalization based on publisher, product, and version
**Normalization Suggestion** - Provided when there is variance between standard normalization and a discovery model that has been manually normalized.
**Machine Learning Normalization** - Generates accurate license position from raw discovery data
**Software License Metric** - Used for reconciliation to determine compliance position. Can be defined for users, devices and processes, and cores(=CPU). Metric group decides what license metrics are available, metric groups are tied to publishers.
**License Metrics**
* Per Core
* Per Device
* Per Named Device
* Per Named User
* Per Processor (CPU count)
* Per User
* It is possible to create one's own custom software license metrics

**Client Access Licenses (CALs)** - Controls number of devices that can access particular software version. If access is purchased for 25 concurrent CALs, then the organization can only have 25 devices or users accessing the service concurrently.

**True-up cost** - Cost that is needed to be compliant. So avg price of license * amount of licenses. During true-up process the required licenses are acquired.

**License change projection** - Estimate of required licenses after change.
* The functionality requires plugin com.sn_samp_change
* The plugin populates [samp_software_change_projection] and [samp_ci_projection_summary] tables when a job is executed. Process is facilitated by event [sn_samp.software_projection]

**Operational integration** - integrating SAM practices into other operational processes

## Software catalog and sourcing

**Purchase Order** - Created when requested items are sourced

**Automatic allocation of software** can be set by setting the worflow of the related catalog item to **Procurement Process Flow - Auto allocation enabled**

**Details included in downloadable Entitlement import template**
* Publisher Part Number - Identifies software model. If not available, next four fields are mandatory.
* Publisher - ex. "Microsoft"
* Product - ex. "Office 365"
* Version - ex. "2022"
* Edition - ex. "Professional"
* Platform - ex. "Windows"
* Language
* Agreement type - Optional, used if agreement type field is linked to publisher-specific program
* PO Number - Field available for just for your reference, if needed
* License type - ex. Full = Base license, or "Upgrade" - update previous entitlement
* Purchased Rights - Number of rights purchased
* Unit cost - Optional. Cost per entitlement right.
* Metric Group - Required. Refers ServiceNow metric group that aligns with publisher packs. ex. Oracle/SAP/Microsoft
* License Metric - Specific metric to be used based on the provided metric group
* Start date
* End date
* Asset tag - optional. Not commonly used for transactional software, but allows tracking large purchase entitlements,
* Owned by
* Company
* Location
* Vendor
* GL Account - Optional. General ledger against which purchase was made
* Cost center - Cost center that purchased the entitlement
* Department
* Named user type - required if Metric Group is “SAP” and License Metric is “Named User”
* Unlimited license 

## Discovery

**Phases**
* **Scanning** 
    * “Are you there? How will I classify you?”
* **Classification** 
    * “How should I classify you specifically?”
* **Identification** 
    * “Have I seen you before?”
* **Exploration**
    * “What else can you tell me about yourself?”

Patterns are used in last two phases.

## Software Remediation

Purpose is to maintain compliance, optimize spend, and support software audits

**Remediation options**
* If software model is **not compliant** four remediation options are available
    * Purchase rights
    * Create allocations
    * Remove allocations
    * Remove unlicensed installs

**Asset Reclamation Request** - Used for example as a part of employee offboarding

## Roles
* sam_user - often needed to work with tasks
* sam_admin - required to opt-int for content services

## Specifics

* SA entitlements = Software Assurance entitlements. Is related to Microsoft Software Assurance 

## Strategic conformance

* Terms
    * **Downgrade rights** - Entitlement rights to use previous or future versions of a software product
    * **Software usage record** - Track sum of software usage on monthly basis
    * **Software reclamation rule** - Used to aggregate usage records and identify unused software

**Software Product Lifecycle**
1. Pre-release
    * Internal: Software purchased
    * Publisher: Release announced
2. General availability
    * Internal: The date when software becomes available
    * Publisher: When available to market
3. Upgrade
    * Internal: When upgrade become available to organisation
    * Publisher: -not available-
4.  End-of-life
    * Internal: The date software will no longer be available to request
    * Publisher: The date the software will not be marketed, sold or improved
5. End-of-support
    * Internal: Date when software will be only supported by internal support teams
    * Publisher: Date after which only security and reliability fixes are provided
6. End-of-extended-support
    * Internal: Date when software will not be supported (even by internal support teams)
    * Publisher: Date after which not even security or reliability fixes are not provided

If a discovery map does not have software product lifecycle content associated with it, **SAM - create lifecycles**, weekly Scheduled job, creates the content.

Content library provides lifecycle content.

**Downgrading software** - purchasing rights for one version of a product but using earlier version.

**Upgrading software** - purchasing rights to one version and being allowed to use a newer version.

If downgrades and upgrades are associated with entitlement, they will be considered during reconciliation. If they are associated with the model, they are tracked for all entitlement rights for that model.

**Technicalities**
Downgrade rights correspond to a discovery map. Weekly scheduled job (Download software content: Downgrade Rights) gets the rights from a content service and pushes data to [samp_dmap_downgrade_model]-table. Then another scheduled job (SAM - Create downgrades/upgrades for a software entitlement).

Downgrade rights can't be deleted but they can be deactivated. no duplicate downgrade rights are not allowed by the system.

## Software installation optimization

**Removal candidates** can be:
* Reclamation candidates - installations that are identified as low utilization
* Restricted software installations
* Other candidates - Installations that are removed due to being unlicensed or unallocated

**States of removal candidates**
* Attention required
* Ready - can be continued, clicking **Reclaim** button advances the workflow
* Awaiting user
* Awaiting approval
* Awaiting Revocation - Waiting for weekly scheduled job (Updating Existing Reclamation Candidates) to run to remove software.
* Closed Complete
* Closed Skipped

**Reclamation**
Softwares become reclamation candidates after they have been unused for a defined period of time.

Reclamation rules aggregate data based on **total usage time**, this can be modified to aggregate data based on **last date used**

**Client Software Distribution (CSD)** is a product that is used to remove/reclaim software. Its full use requires "Orchestration - Client Software Distribution" plugin (com.snc.orchestration.client_sf_distribution) that belongs to ServiceNow Orchestration -product. However, the functionality to revoke software / reclaim license is included in SAM Pro.

To utilize revoce and reclaim, SCCM configuration record is needed that identifies:
* The application
* The uninstall collection
* associated software discovery model

## Software Retirement

**Software Lifecycle Report** identifies  products nearing end-of-life, end-of-support and end-of-extended support
* Report is based on scheduled job **SAM - Get install count for software model** and requires role [sam_user] or [model_manager].

## Reporting
**Overview Dashboard** - Software asset true-up costs and license, compliance, and removal summary trends.
**Publisher Dashboard** - Compliance analysis related to Microsoft, Oracle, IBM, VMware, and Citrix. 
**Subscription Dashboard** - Compliance analysis results related to Microsoft Office 365 and Adobe Cloud License Management
* Other dashboards
    * Software Asset Analytics
    * Software Asset > SaaS Overview
    * Engineering License Overview 
        * Engineering License Manager application provides visibility into license usage for engineering software applications (for ex. AutoCad, ESRI) by using integration with OpenLM
    * Software Asset Workspace > Renewal calendar
    * Software asset success portal


## Domain stuff

* sys_domain and sys_overrides field
* data separation must be present before process separation
* System Property: glide.ui.domain_reference_picker.enabled = true

Roles
domain_admin
domain_expand_scope

Admins part of 
global and any admins in charge of system wide configurations should be in TOP
 

 What property allows for data separation?
glide.sys.domain.enabled


What property allows for process separation?
glide.sys.domain.delegated_administration

What is the best practice naming convention for business rules that modify other records based on domain changes?
Name contains "Cascade Domain"

What is the best practice naming convention for business rules that handle inserting records without a domain?
Name contains "Domain - Default"


Steps to domain separate a table?
1) Create a domain field
2) Add a Business Rule to set domain
3) Add a Business Rule to set a default domain if the prior step fails
4) Add a Business Rule to cascade related records

Delegated Development with Domain Separation manages which components administrators and developers can modify

glide.domain.session_scope = session domain

data separation with glide.sys.domain.enabled

glide.sys_domain.use_record_domain_for_processes

Multi-Tenant SSO Plugin

Use domain paths instead of domain spooling ( sys_domain ) or domain numbering. Queries that use domain paths are much faster than spooling or numbering.