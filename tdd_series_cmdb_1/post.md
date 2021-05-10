# Applying TDD goodness for cumbersome CMDB integration

## Context
I have a problem on my desk that at first I deemed to be unfit for my current level of ServiceNow TDD mastery. However, when doing the development I noticed myself spending quite much time debugging, and I figured that TDD would benefit there.

So instead of doing random background scripts and clicking around the instance to see if the solution works, I could just do the test and run that each time. Do'h.

## The problem
There is a CMDB integration plugin for ServiceNow made by another CMDB software provider. We are utilizing that to transfer data from another configuration database to ServiceNow. As one might guess, there are some issues with the plugin, and now I need to investigate the source code of the plugin to understand the workings and produce a fix.

## TDD approach
I started solving this problem by repeating this cycle plenty of times
1. Tweak configurations
2. Reprocess import set
3. Run transform 
4. Check outcome and logs
5. If desired outcome was not achived, back to step one

However, I should be able to test my configurations faster by proceeding 
1. Build a test step to do a specific operation with declarative error logging 
2. Tweak configurations
3. Run test and check results
4. If desired outcome was not achived, back to step two

## ATF Technicalities
### Testing regex match of operating system
#### Test step of choice
Run server side script
#### Test configurations
No biggie. Call the script include function with a mockup gliderecord that is similar to the one in import set. Assert that new type of OS is returned
### Testing Success of transform script
#### Test configurations
Not as trivial. GlideScopeEvaluator API provides a nice way to test transform script *without* copying its contents into test configurations. So in the test step configurations we need to query gliderecords inorder to pass them to the function defined in transform script:

pastecode here
