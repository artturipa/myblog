### Delete Flow Designer Custom Action
Delete record from table **sys_hub_action_type_definition**

### Do stuff asynchronously via synchronous script
Use the **ScheduleOnce** API. Useful also if you wan't to ensure that updates are done as system user.

### Activate new UI (Next Experience) in San Diego -release
Set system property **glide.ui.polaris.experience** to true.

### Find out funciton definition
If you would like to see how a function has been implemented by ServiceNow, you can try:

    gs.info(FUNCTION_NAME)

However, if the result is __[native code, arity=<number>]__, it can't be accessed.

Note also that before trying this you should try global code search via Studio.

### Ensure that emails are shown in activity journal

Most common mistake is that user's role is missing from property: **glide.ui.activity.email_roles**. In addition, email sending should be active in the instance. Emails with Sent-Ready -status are not displayed in the activity journal.

### Check if in portal

Check if user is from portal, might be usable in advanced ACLs or in view rules:

    var isInPortal = gs.action.getGlideURI().toString().startsWith('api/now/sp');

### Check syntax macros

Type "help" and press tab in SN syntax editor to display available macros.

### Avoid DateTime conversion issues

When doing logic for user interaction, use .setDisplayValue for GlideDateTime to prevent problems with differing time zones.


### Change instance logo in Polaris UI / Next experience

edit properties **glide.product.image** and/or **glide.product.image.light**. [More on Docs](https://docs.servicenow.com/en-US/bundle/sandiego-platform-user-interface/page/administer/navigation-and-ui/concept/c_ModifyTheBanner.html).

Enable highlighted values in Next Experience:
In **sys_highlighted_value**, Remove value from **workspace** attribute.

### UI Action Visibility exists

Table **sys_ui_action_view** provides a simple way to configure which UI Actions are shown in a view. You need to do the record to same scope where the UI Action in question is. And to find out the right UI Action, one can find the sys_id with browser's developer tools in page DOM. Sys_id of the UI Action is the **gsft_id** attribute of the corresponding **&lt;button&gt;** -element

### Monitor user transactions that happen in workspace

Useful, if you need to backtrack which users have opened which records. Logs are stored in **syslog_transactions**, look for module **Transactions (All)** in application navigator.
 
### Build process to ensure CMDB data is up to date

It might be hard to decide whether a record in CMDB is up to date. Even if details of a record have been checked, no value has necessarily changed. ServiceNow has **Data Certification** application which creates tasks to validate data, and via these tasks one can ensure that CMDB is up to date.

### Set calendar's week start on Monday (or any other day)

Server side:
    data.userLanguage = gs.getSession().getLanguage();


Client side
    moment.updateLocale(scope.data.userLanguage, {
        week: { dow: 1 } // Set to one, if Monday is desired
    });

### Circumvent terrible slowness of Decision Table's

The API provided by ServiceNow is terrible. It takes several seconds to complete with few hunderd rows. Forget the API, and build direct gliderecord query to actual table behind decision table (such as sys_decision_question).

### Get sys_id of record to be generated in catalog client script:

    if(parent.angular) { 
5 | 	var sysIdOfNewRecord = parent.angular.element("#sc_cat_item").scope().data._generatedItemGUID; 
6 | } 

## Change "STARTSWITH" default search to "CONTAINS" in reference variables

1. Disable the glide.ui.ref_ac.startswith system property
2. Create new user preference for the refernced table and leave user empty. Name of the user preference: "REFERENCED_TABLE.autocomplete.contains"

### NiceError exists, and it gives a stack trace

    var msg = new NiceError("Your log message")
    gs.info(msg);

Kudos to [Luke from Community](https://www.servicenow.com/community/developer-articles/use-niceerror-to-generate-better-log-messages/ta-p/2404286)

### Updates from apprepo are missing??

They are most likely skipped due to modifications in prod. Check and activate skipped updates from **sys_upgrade_history**

### Next Experience only for some users

Set these properties
* glide.ui.polaris.experience (true/false) = true
* glide.ui.polaris.on_off_user_pref_enabled = true

Also, create an user preference
- glide.ui.polaris.use (string) = false (This sets so that Next Experience is disabled by default)

After these steps, users can find "Turn on Next Experience" from user preferences / display.

### Control Next Experience Top Bar links

**sys_polaris_menu_config_list**

### license_role table exists and is great

Check that out asap. There one can see whether a role is counted as fulfiller, business stakeholder or requester. 