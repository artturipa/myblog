# Dashboards into portal for end users

## Introduction

Most reporting in ServiceNow is done for Service Managers, Process Owners, Top managementor other internal stakeholders. Reports are also useful for the end users. As an example, you can enhance customers' experience by providing them with __Expected Resolution Time__ or __Queue Length per Service__. 

More than once I have encountered a belief that browsing reports would require a fulfiller license. That belief is false. End users can browse reports without Performance Analytics subscription, often they just are lacking the interface to do so. 

Service Portal is the most common way end users use ServiceNow, so end users should be able to find their reports there. To achieve that, ServiceNow provides us with configurable -report widget, but with it each report needs to be hard coded to a portal page. That approach suits only individual use cases. 

So here comes a scalable approach to the problem. 

## Solution overview

The solution is a bit dirty due to iframe, but I feel no shame as it gets the job done. With this approach, end users have "__Reports__" tab available in the portal's navigation bar. The link takes the user to a page, which shows all the dashboards shared with the user. Each visible dashboard acts as a link, which again takes the user to a specific portal page showing the dashboard contents.

## Configuration steps

* Add the "Reports" link to navigation tab. (check in __sp_rectangle_menu_item__)
* Create a portal page to show available dashboards 
* Create a widget which shows dashboards visible to customer 
* Create a portal page to show the dashboard contents
* Create a widget which shows dashboard content

## Configuration tips

**Dashboard browser widget**

HTML

      <a class="col-lg-3" ng-repeat="dashboard in c.data.dashboards"
         href="{{'portal?id=dashboard&sys_id='+dashboard.guid}}">
        <span ng-bind="dashboard.title"></span>
      </a>

Server Script

    var grDashboard = new GlideRecordSecure('pa_dashboards');
	grDashboard.query();
	var dashboards = [];
	while (grDashboard.next()) {
		if (!grDashboard.name) continue // User has no access --> Skip
		var dashboardObj = {};
		dashboardObj.name = grDashboard.name.toString();
		dashboardObj.guid = grDashboard.sys_id.toString();
		dashboards.push(dashboardObj);
	}

**Dashboard content widget**

HTML

    <iframe style="overflow: auto; height: 750px; width: 100%;"
            src="{{c.data.dashboardLink}}">
    </iframe>
    
Server Script

      data.dashboardLink = "/$pa_dashboard.do?sysparm_dashboard="+$sp.getParameter("sys_id");

## Sharing reports to end users

* Create a dashboard, share it to audience "**public**"
* Set the visibility of reports in the dashboards to "**Everyone**"

## Going back to the licenses

Reporting is all good. However, only licensed users can browse details of the record. These two principles sometimes collide, and therefore ServiceNow prevents __list__-type of reports from end users =).