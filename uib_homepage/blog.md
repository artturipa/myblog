# What?

ServiceNow's fulfiller UI traditionally has boring and useless landing page, here a way to improve it.

## Create the page

Of course with UI Builder, as it starts to be fantastic. Most of the bugs have been fixed.

So:
1. Create new Experience
2. Use **Workspace App Shell**, as it has same top level navigation that is visible elsewhere in the platform
3. Create new page from scratch. Recommended name: **home**

## Ensure end users have access to the page

It seems that ServiceNow is now able to create the ACLs automatically, so it should be sufficient to grant users **canvas_user** role. Nevertheless, you can check that there exists an ACL with type: **ux_route** and name **COMPANY_PREFIX.EXPERIENCE.\***

## Stylize the page

If you like, you can start by adding a background image for the langing page:
1. Navigate to db_image
2. Upload and name the image.
3. In UI Builder
    * Select "Body" / "Styles" / "Advanced" / "Edit CSS"
    * Define background, image can be referenced with __url("FULL_NAME_OF_THE_IMAGE_JUST_UPLOADED")__
       

Proposed initial CSS for body:
   
    min-height: 100%;
    background: rgb(var(--now-color--neutral-1));
    background-image: linear-gradient(rgba(var(--now-color--neutral-1),0.5), rgba(var(--now-color--neutral-2),0.5)),url("FULL_NAME_OF_THE_IMAGE_JUST_UPLOADED");
    background-repeat: no-repeat;
    background-size: 100%;


If there exists white paddings outside the image, try turning Bare setting on and off from **page**, and save in between.

## Add Content to the page

This one is up to you and your use case. Do consider adding a simple list component to show user's active tasks.

To open the task from the component, use **link to destination** with following configuration:

    function evaluateEvent({api, event}) {
        return {
            route: null,
            fields: null,
            params: null,
            redirect: null,
            passiveNavigation: null,
            title: null,
            multiInstField: null,
            targetRoute: null,
            external: {
                url: "/now/nav/ui/classic/params/target/" + event.payload.table+"/.do%3Fsys_id%3D"+event.payload.sys_id
            },
            navigationOptions: null
        };
    }

To explore other parameters refer to documentation [here](https://developer.servicenow.com/dev.do#!/reference/next-experience/xanadu/shared-components/now-record-list-connected-snapshot/uib-setup) and community [here](https://www.servicenow.com/community/developer-forum/ui-builder-how-do-i-link-to-a-destination-and-pass-parameters/m-p/1861450).

## Make the page default
Landing page is controlled by user preference (__sys_user_preference__) **my_home_navigation_page**, (some instances also have **homepage** property, check that if not working). You can set the landing page to be default for all users, by leaving the user field empty and set system value to **true**.

Format for the value shoule be /x/PREFIX/APP/PAGENAME

 ![Graph](https://raw.githubusercontent.com/artturipa/myblog/main/rest_cache/cahcegraph.png)

 ## Debugging tips

 As of writing this, ServiceNow had still some bugs after all. My events were triggering multiple times when that should not be the case. In order to track down the events and remove them, do recognize that the contents are both in *sys_ux_macroponent* and *sys_ux_screen*. If event triggers multiple times, ensure that only one instance of it exists in **sys_ux_screen**.