# Stupid things in workspace configuration 

Note that these notes refer to configurable / UI Builder Workspaces.

## Editing lists

Needs to be done in **sys_ux_list_menu_config**.

## Editing views, list layout and related lists

Just edit the default view in classical UI. However, if the changes are not applied to workspace, check the views in table **sys_ui_list** or **sys_ui_view**.

## Editing m2m -relationship form contents

To rename the header, rename m2m-relationship table's label (**sys_db_object**)
To rename sections in form, rename form sections (**sys_ui_section**)

## Hiding second instance of journal fields

If you wan't to have journal fields on your form, you are going to have the same fields in two places. In the 'form part' itself, and in the comments section. You can do workaround, by moving the journal fields into their own __form section__, and then hiding the section via UI Policy / Client script. This way the journal fields are only visible in the Comments -section. 

## Rename Form Section
Especially in m2m relationships this looks like s**t. To rename it as something useful, do this:

1. Goto: sys_ui_form_section
2. Create new reference to col sys_ui_form
3. Create new reference to col sys_ui_section
4. Give a more meaningful name

## Add UI Action to custom table

They are not UI Actions, look up **UX Form Action**

## Theming

Check this out
https://docs.servicenow.com/bundle/quebec-application-development/page/administer/ui-builder/concept/work-themes.html 

## Lists not loading

Try adding **canvas_user** role to the users using the workspace. Then create record in **sys_ux_applicability_m2m_list_list** for each list link, and make them refer to same list applicapility **sys_ux_applicability**, which can be created in the process.

Thanks to user barry, more discussion here:
https://community.servicenow.com/community?id=community_question&sys_id=4b6e88c3dbbd30d4fb115583ca9619ad 


## Delete experience

Remove from **sys_ux_page_registry**

## Specify content in form headers

Do it via table **sys_aw_form_header**, you might need to touch records in **sys_ux_header_config** and **sys_ux_m2m_workspace_header_ux_header_config** as well.

Note that in **sys_aw_form_header** there is Workspace attribute, which is not visible out of the box. Add it to the form and clear the value.

## Control Access to configurable workspace

Create following ACL:

* Type = ux route
* Name = APP_NAMESPACE.COMPANY_PREFIX.APPSCOPE.home (for example: x.1232.booker.home)
* Operation = Read
* Role = add required roles

## Highlighted values from old to new workspaces

To be done in **sys_highlighted_value**. Clear the value in "workspace" attribute.

## Remove "+"-icon which suggests creating new records

Look for records with "Description = Tabs Configuration" in table **sys_ux_page_property**, and modify the JSON. 

The value to be: 

    {
    "contextual":[
        "record"
    ],

    "maxMainTabLimit":10,
    "maxTotalSubTabLimit":30
    }

## Edit List actions such as "Assign to Me" or "New"

Check **sys_declarative_action_assignment**

## Hide list actions such as "New"

Open **sys_declarative_action_assignment** and search for records defined for **global** table and **list** . Then open the relevant record and check related list Action Exclusions **sys_workspace_declarative_action_exclusion**, add record there.

Note that you can't select tables from scoped apps to be excluded. However, you can create a new exclusion record, and force the table name with background script to be the table you want from scoped app. Outcome seems to be the same, but it definitely isn't a good practice. 

## Fix notifications

From related lists "Contents", add new content and mark it as Workspace.

## Enable workspace notifications for larger user groups

Increase the value of property: **glide.ui_notification.max_recipients**

## Copy pages or edit page properties when UI Builder does not work

Check out **sys_ux_macroponent**

## Change page path when UI Builder does not work

Check out **sys_ux_app_route**

## Enable Edge Encryption to work in workspace lists

At least in Tokyo -version, there is still a bug which makes it impossible to decrypt values in list components. 

It is possible to circumvent the problem by setting following properties:

* glide.ui.list.batching.exclusion = list the tables considered
* glide.uxf.lib.batchGQLEffectRequests = false
* glide.uxf.lib.classic.batchGQLEffectRequests = false

## Edit details in contextual sidebar

This needs to be done via UI Builder.
1. Open workspace in UI Builder
2. Navigate to record -page
3. From right part of the page, look up contextual sidebar
4. Open the specific sidebar and make changes there

If UI Builder bugs and does not allow you to save, edit JSON in the record via platform UI, table **sys_ux_macroponent**. 

## Create new overview tab to record page, or edit an existing one

The details live in table table **sys_ux_screen_type**, so you can check existing logic and try to reverse engineer that.

The steps are something like below. Detailed instructions in [this great video by Naveen](https://www.youtube.com/watch?v=3V8yWfdAf48).

1. Create a new page, and set parameters to table and sys_id
2. Navigate to **sys_ux_screen_type** and create new record, name it for example **TABLE_LABEL overview collection** 
3. Navigate to **sys_ux_app_route** and select previously created record as **screen collection**, and set **Route** to the value that the automatically created UX App Route has.
4. Create new record for **sys_ux_screen** and set the newly created page for **page definition**, and parent macroponent to where the page wants to be rendered, so **record page tabs**.

Note that the label of the tab comes from name of the record in **sys_ux_app_route**. One might has to change label for the change to take effect.

## Change default landing page

Change landing path in **sys_ux_app_config** to page's path. If it does not work, change also route in **sys_ux_app_route**. For me, the change did not take effect immediately.

## Edit side links / navigation

This, again, is an extremely stupid thing I spent 30 minutes debugging. Usually the setting is found via UI Builder in "Edit experience settings". However, in some instances that setting is missing. 

In those cases, locate the links via **sys_ux_page_property**, look for **chrome_toolbar**, and edit JSON in Value field.

## Edit content and labels displayed in workqueue -page (IRM workspace)

Here: **sn_grc_workspace_applicable_table**

## Open form and prepopulate it with query values:

To Workspace UI Action, put following:

    var query = 'column_name_here=' + 'value_here';
    g_aw.openRecord(tableName, '-1',{
        query: query
    })


## Fetch information via script from data resource

The outcome might be stored either to **output** or **results** -property. 

Like this:
    api.data.DATA_RESOURCE_NAME.output.data...
    api.data.DATA_RESOURCE_NAME.results.data...

You might need this if you wan't to use the outcome as a scripted property value. Then the outcome needs to be assigned to client state parameter via data resource events, which is then passed on to the component. 
