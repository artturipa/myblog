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