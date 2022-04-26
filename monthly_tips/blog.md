## January

### Delete Flow Designer Custom Action
Delete record from table **sys_hub_action_type_definition**

### Do stuff asynchronously via synchronous script
Use the **ScheduleOnce** API. Useful also if you wan't to ensure that updates are done as system user.

## February

### Activate new UI (Next Experience) in San Diego -release
Set system property **glide.ui.polaris.experience** to true.

### Find out funciton definition
If you would like to see how a function has been implemented by ServiceNow, you can try:

    gs.info(FUNCTION_NAME)

However, if the result is __[native code, arity=<number>]__, it can't be accessed.

Note also that before trying this you should try global code search via Studio.

### Ensure that emails are shown in activity journal

Most common mistake is that user's role is missing from property: **glide.ui.activity.email_roles**. In addition, email sending should be active in the instance. Emails with Sent-Ready -status are not displayed in the activity journal.

## March

* Nothing learnt, I was skiing.

## April

Check if user is from portal, might be usable in advanced ACLs or in view rules:

    var isInPortal = gs.action.getGlideURI().toString().startsWith('api/now/sp');

Type "help" and press tab in SN syntax editor to display available macros.

When doing logic for user interaction, use .setDisplayValue for GlideDateTime to prevent problems with differing time zones.