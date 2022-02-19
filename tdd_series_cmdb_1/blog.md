# Applying TDD goodness for cumbersome CMDB integration

## Context
I hoped I could apply TDD development to all things in ServiceNow. But now the amount of more crucial issues and deadlines have shifted my focus elsewhere. However, I have encountered few situations where TDD is a necessary step to ensure the initial implementation can be done efficiently.   

## The problem
There is a SNOW <-> ServiceNow -CMDB integration plugin for ServiceNow (SNOW does not refer to ServiceNow, but to Snow Software). The plugin is utilized to populate CMDB in ServiceNow with the data from SNOW. As one might guess, getting just the basic integration to work has its usual set problems. Add there the customer requirements to modify & control data and you have a good chunk of high tier ServiceNow configuration to tackle. The 3rd party plugin adds its own flavor to the situation, as one needs to investigate its source code in order to understand the solution being configured.

No biggie. That's what I am paid to do, and I know how to do it. And because the situation is rather complex, sophisticated development practices should be applied to reduce development inefficiency.

I noticed myself spending increasing amount of time for debugging. Here TDD would actually fasten the development. So instead of doing random background scripts and clicking around the instance to see if the solution works, I could built a fitting test and run it after configuration changes.

## Changing the approach towards TDD

When doing the implementation, at first I repeated this cycle x times.
1. Tweak configurations
2. Reprocess import set
3. Run transform 
4. Check outcome and logs
5. If desired outcome was not achived, back to step one

After the manual debugging had caused enough frustration, I changed the approach.
1. Build a test step to do a specific operation with declarative error logging 
2. Tweak configurations
3. Run test and check results
4. If desired outcome was not achived, back to step two

This is a huge win. Running the import manually to test each change is a pain in the a**. 

## Tips to build the ATF step test

* In situations as complex as this, you should build the test via script. Utilize "_Run server side script_" -step
* Create mock-records to use in the test as GlideRecords. So don't worry if you won't have an actual record in a table. Initialize a GlideRecord and define the attributes consumed by the test.
* Pass the mock-record into any Script Includes that need to be tested.
* For any other scripts, utilize *GlideScopeEvaluator API*, it allows you to test transform, or other, scripts without needing to copy the scripts elsewhere.