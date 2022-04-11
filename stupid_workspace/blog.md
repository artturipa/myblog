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

Try adding **canvas_user** role to the users using the workspace. Then create new list applicability -record in **sys_ux_applicability_m2m_list_list**

Thanks to user barry, more discussion here:
https://community.servicenow.com/community?id=community_question&sys_id=4b6e88c3dbbd30d4fb115583ca9619ad 


## Delete experience

Remove from **sys_ux_page_registry**