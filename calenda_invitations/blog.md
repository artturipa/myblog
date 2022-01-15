
# Short Summary

In case you need send calendar invitations via email, the steps are not as intuitive as one could hope. Below short summary of steps that are needed. More comprehensive instructions can be found through ServiceNow Community, official docs are insufficient.

## Steps

1. Create event in event registry __Note that other conditions are just as viable, in this use case I'm triggering the event via portal widget, hence this condition__
2. Create notification, set the send condition to the event.
* Configure notification
    * Type = Meeting invitation
    * What it will contain / Content type = Plain text only
    * Define email template

* Configure email template
    * Message text
        BEGIN:VCALENDAR
        PRODID:-//Service-now.com//Outlook 11.0 MIMEDIR//EN
        VERSION:2.0
        METHOD:REQUEST
        BEGIN:VEVENT
        ATTENDEE;RSVP=FALSE:MAILTO:${to}
        ORGANIZER:MAILTO:${from}
        DTSTART:${dtstart}
        DTEND:${dtend}
        LOCATION:${location}
        TRANSP:OPAQUE
        SEQUENCE:${sys_mod_count}
        UID:${number}
        DTSTAMP:${dtstamp}
        DESCRIPTION:${description}
        SUMMARY:${summary}
        PRIORITY:5
        X-MICROSOFT-CDO-IMPORTANCE:1
        CLASS:PUBLIC
        BEGIN:VALARM
        TRIGGER:-PT30M
        ACTION:DISPLAY
        DESCRIPTION:Reminder
        END:VALARM
        END:VEVENT
        END:VCALENDAR

    * Note that it is not clear where ${  } -notation refers. For example MAILTO:${to} refers to 'to' attribute of the email itself. ${dtstart} referst to Import Export Map, which is explained below. The same notation can also be used to refer fields in the table. Such as DESCRIPTION:${description}, one can also take text from multiple fields LOCATION:${location} - ${location_detailed}.
    * There are multiple useful settings one can configure to the template. More details can be found via icalendar specifications. https://datatracker.ietf.org/doc/html/rfc5545

* Create and configure Import Export Maps (sys_impex_map)
    * Set table, name and description
    * Name = TABLENAME.icalendar _this needs to match precisely, with scoped tables you might need to make the dictionary entry longer_
    * Type = icalendar
    * Save and continue to field maps

* Create and configure Import Export Map's field maps
    * Type = field
    * Here External names need to match to what reads inside ${  } -notation in defined calendar template
    * You need to define atleast dtstart and dtend here. They can be mapped to datetime fields in the table.

* Set logic to send email 
    gs.eventQueue(EVENT_NAME,GlideRecord)
