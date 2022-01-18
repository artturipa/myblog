# ServiceNow Instance Security Center

ServiceNow provides an instance specific portal about instance security, known as Instance Security Center (ISC). It can be located in every instance __**instancename.service-now.com/isc**__.

ISC shows plenty of useful information and links, from recent events to security hardening.

## Monitored Security Events

ISC shows Performance Analytics graphs about the volume of security events. The volumes displayed by chart are retained for a long time, but in case you need to do any investigation about a specific log entry, the actual logging record is needed.

As a default log records are cleared each week, so if you need to check historical data going futher back it's not possible.

Luckily there exists a simple fix for the issue. The clearing logic is defined in Scheduled Job **AppSec - Clear Weekly Events**, there you can control how many days log entries are retained.

Taking into account that the amount of records on the table should be relatively small, there shouldn't come any performance issues to worry about when increasing the retention time. You wan't to extend log retention for the table **appsec_security_dashboard_event_logs**.

Below a paste from Job contents, which shows how you can extend the log retention to 6 months.

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

1. Define acceptable level for different event volumes
2. Create email digest about registered events and log contents.
3. Plan ahead what should be the actions taken when volumes exceed acceptable level.s