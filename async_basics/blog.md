# Async - why

If are not familiar with basics of asynchronous operations, here is a quick summary. When designing solutions, we can do operations in two different ways:

**Now - synchronously**
Or
**Later - asynchronously**

When operations are done synchronously, they are processed immediately before the processor is assigned new jobs from the job queue. When operations are done asynchronously, the operation in question is put to queue to be processed later on.

There are many reasons to do things asynchronously. In ServiceNow development the most common reason for that is that we don't want halt other operations to wait for processing that could be done later. For example, when user submits a catalog item, we do not need to wait that the item is processed and integrated to vendor's application before directing user to 'request submitted'-page. In ServiceNow, perhaps most common reason for async operations is to smoothen user interaction.

### Async - how

In ServiceNow there are many ways to do async operations, of which the most common are:
* Async Business rules
* Scheduled Jobs
* Flows
* Events

## Example

Recently I built a simple functionality to track number of attachments on a record. It was done by adding a new field to task-table and a Business rule that checked and saved amount of attachments whenever there were changes made to that record's attachments. Easy peasy.

This is the type of scenario that should be done asynchronously. Otherwise we would add multiple function calls and delay to __every attachment change on all task types__ to the entire instance. The delay would be minimal. However, these type of decisions can accumulate over time, resulting in overall slowness in the instance.

## Configuration tips

### Async Business Rules
Even though the requirement and the implementation was simple for the aforementioned example, I had some problems with it. The problems were due to me not remembering basic steps or due to poor documentation from ServiceNow. Below few tips for the next time:

**Not executing or just error?**
I spent some time debugging why the business rule is not executing. Then it turned out that the business rule was actually executing, but there was a server error in my script. What surprised me there ws that the server error was not logged into system logs, as it would be in synchronous operations. So **remember that server errors are not logged from async business rules**.

To avoid these types of problems, adopt a standard to utilize try catch in every async (or in all) business rules:

    let gl = new global.GSLog("APPNAME.report.log", "SOURCE_LABEL");

    try {
        // Your code here
    catch (e) {
        gl.logErr(`Error in Business Rule NAME_OF_RULE
            Message: ${e.message}
            Linenumber: ${e.lineNumber}
            Stack: ${e.stack}`);
        }

Of course it could also be that the business rule is not executing at all. Then ensure that there are no rules that execute earlier and set **setWorkFlow(false)**. It can be easily debugged with Script tracer.

**Triggering on Delete Operations**

It is common knowledge that async Business Rules do not have access to **previous**-object. However, do consider that if the rule triggers from delete-operation, it does not have access to **current**-object neither. That may lead to issues.

In these occasions, if details from the record are required for the operation, it is beneficial to utilize event and script action -pattern. So instead of doing the operation in async Business rule, make a synchronous Business rule that fires an event, and then a **script action** that is triggered by the event does the heavy lifting.

Code snippets:

Business Rule

    try {
        // Here second parameter is null, as there could be the gliderecord but as the rule is triggered by delete, gliderecord does not exists when event is processed
		gs.eventQueue("event.name",null,current.getValue('field_to_pass_as_parameter'));
	} catch(e) {
		gl.logErr(`Error in Business Rule NAME_OF_RULE
            Message: ${e.message}
            Linenumber: ${e.lineNumber}
            Stack: ${e.stack}`);
	}


Script Action

    var field_value_passed_as_parameter = event.parm1.split(",")[0]

    processFunction(field_value_passed_as_parameter)
    function processFunction(field_value_passed_as_parameter) {
        // logic here
    }


### ScheduleOnce API

This is not a well known feature. I found it handy when I had to ensure that automated comments were given from system user and not from the user that executed the transaction.

This of course is useful for other types of async as well.

    var util = new yourScriptInclude();
    var scheduler = new ScheduleOnce();
    // Below script is basically: (function)(arguments)
    scheduler.script = '('+util.functionName+')("'+variable_to_pass_as_first_parameter+'","'+ variable_to_pass_as_second_parameter+'");';
    sched.setAsSeconds(30); // delay in seconds
    sched.schedule(); // pushes the script execution to sys_trigger


