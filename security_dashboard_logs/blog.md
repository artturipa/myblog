# ServiceNow Instance Security Center

ServiceNow provides an instance specific portal on instance security: Instance Security Center (ISC). It can be located in every instance __**instancename.service-now.com/isc**__.

ISC shows essential security events and provides guidance on security hardening. You should check that out.

## Monitored Security Events

Security event volumes are shown in Performance Analytics graphs. The volumes themselves are retained for a long time, but the source data is wiped frequently. So if you would like to do investigate a specific log entry in the past, you are in trouble. As a default log records are cleared each week.

Luckily there exists a simple fix for the issue. The clearing logic is defined in Scheduled Job **AppSec - Clear Weekly Events**. This job controls how many days log entries are retained.

The amount of records on the table is relatively small, so there shouldn't be any performance issues to worry about if the retention time is increased. 

Below a paste from the job contents, which shows how you can extend the log retention to 6 months. You wan't to extend log retention for the table **appsec_security_dashboard_event_logs**.

    // Constants
    var constants = new ISCConstants();

    // Clear domainset
    var gr = new GlideRecord(constants.tables.DOMAIN_RESULT_SET);
    gr.addQuery('sys_created_on', '<', gs.daysAgoStart(7));
    gr.deleteMultiple();

    // Clear dashboard event logs
    gr = new GlideRecord(constants.tables.SEC_DASHBOARD_EVENT_LOG);
    gr.addQuery('sys_created_on', '<', gs.daysAgoStart(6*31));
    gr.deleteMultiple();

    // Clear security notifications
    gr = new GlideRecord(constants.tables.SEC_NOTIFICATION_LIST);
    gr.addQuery('sys_created_on', '<', gs.daysAgoStart(7));
    gr.addQuery('read', true);
    gr.deleteMultiple();

Please note that not all security events are kept in the table **appsec_security_dashboard_event_logs**. Antivirus and email related event logs are stored in different tables.

## What next

In order to get most out of ISC and step up your instance security, following steps should be considered:

1. Define volume thresholds for security event.
2. Configure a notification to notify relevant stakeholders when threshold is exceeded.
3. Plan ahead what should be the actions taken when volumes exceed acceptable levels.
4. If you are not happy with the threshold approach, create email digest to send you weekly overview about security events.