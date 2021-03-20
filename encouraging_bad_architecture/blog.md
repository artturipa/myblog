# How current ServiceNow licensing encourages bad architecture

## What I don't like about custom table licensing
There is something I don't like about Servicenow's current licensing policy. During the Madrid release Servicenow made a major update to its licensing model and started counting amount of custom tables. Earlier it was possible to build any number of custom applications with any number of custom tables. 

It's understandable that Servicenow sought a change to a situation, where customers were able to gain extraordinary value with only a minor increase in license costs. If a customer starts to manage ten additional workflows with the platform, it is only reasonable that Servicenow wants some compensation about the increased usage.

## The problem
Currently there is a limit set on amount of custom tables. I never liked that approach. Table amount does not necessarily reflect the scope of ServiceNow's usage in an organisation. And as customers, developers and managers are aware of the license effects, they can always hack the system by building new workflows without creating new tables.

Additional tables can be avoided by utlizing complex multipurpse tables. So rather than having its own table for each different type of object, one can utilize a 'subclass' or 'category' field that is referenced in the configurations. I don't encourage such approach. It creates a structure that is neither easy to build nor manage. Unnecessary complexity puts quality, user experience and the platform at risk. 

## A better Way
Here's an alternative approach. Rather than basing license costs on customers' amount of tables or activated modules in use, invoice them based on the actual value they gaining out of ServiceNow. The licensing could be based on the amount of tasks resolved in the system. This way customers could build new processes and implement additional modules without investment risks. This type of approach would align Servicenow's and its customers interests. 

I believe in capabilities and potential of the ServiceNow platform. And I feel that licensing should be designed in a way that aligns interests of both parties. That is how long and floursihing partnerships are cultivated.
