# Need for a (reusable) Service Portal

I am employed by a significant ServiceNow implementation partner, and in this work as a ServiceNow consultant I do a lot of implementation projects. 

It has annoyed me that configuring Service Portal seems to be a cumbersome task every time, and the work effort estimates are several man days even if the requirement is to build most basic and simple Service Portal for few catalog items.

There shouldn't be any problems in building a good basic Service Portal that would be reusable for many organisations. ServiceNow's own Out of the box Service Portal is not fit for that, it is crude and it hasn't been updated in years.   

## Opportunity presents itself

In one of my current projects I have the role of a solution architect. I try to avoid doing developer work as much as possible, but sometimes I need to step in.

Now I am faced with a situation that our team is missing a portal developer, and the solution needs a _simple and basic_ Service Portal. 

This is a great excuse for me to step in and build a Service Portal, and do it in such a way that it is reusable in future projects as well.

## Requirements

For the portal to be reusable and good it should fulfill below criteria
* Quick to deploy for different instances 
    (time required should be below 1 MD, ideally 1 hour) 
* Guided setup steps
* Freely Configurable
* Basic widgets and content included
* Extensible
* Pleasant UI & Visual Design

## Solution

To ensure transferability and limit decoupling, the portal is created as a scoped application in ServiceNow.

### Branding and customisation

The portal refers ServiceNow's basic La Jolla -theme, and certain set of CSS variables are defined in CSS variables field of the portal record. When the portal is deployed to a new instance, branding can be configured in the portal record.

### Homepage

A new page is created for homepage. Home page in order to add a custom background to homepage, it needs to be done as a page specific CSS.

Background picture for portal's home page can be set nicely with following css:

    body {
        background: url("imagelocation");
        background-repeat: no-repeat;
        background-position: center 60px;
        background-size: auto 520px;
    }

## Instructions

1. Export latest default portal application
2. Import application to instance
3. Rename name of application to customer's context
4. Edit content what is being displayed on sp_rectangle_menu_item  
5. 