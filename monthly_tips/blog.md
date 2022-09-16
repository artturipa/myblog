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

Type "help" and press tab in SN syntax editor to display available macros.

When doing logic for user interaction, use .setDisplayValue for GlideDateTime to prevent problems with differing time zones.


### Change instance logo in Polaris UI / Next experience

edit properties **glide.product.image** and/or **glide.product.image.light**. [More on Docs](https://docs.servicenow.com/en-US/bundle/sandiego-platform-user-interface/page/administer/navigation-and-ui/concept/c_ModifyTheBanner.html).

Enable highlighted values in Next Experience:
In **sys_highlighted_value**, Remove value from **workspace** attribute.

### UI Action Visibility exists

Table ** ** provides a simple way to configure which UI Actions are shown in a view. You need to do the record to same scope where the UI Action in question is.