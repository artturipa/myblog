# Useful Portal Scripts & Patterns

Here will be some useful patterns and code snippets to use in (angularJS) portal development.

I have included these scripts here foremost to help my own working. But if someone else gains something of value here, even better.

## Building Confirmation Modal
Note, this is well documented by ServiceNow, for more examples check the [reference documentation](https://developer.servicenow.com/dev.do#!/reference/api/sandiego/client/SPModal-API?navFilter=spmodal).

**HTML Link**

            <a href="javascript:void(0);" ng-click="c.modalScript()" />

**Client Script**


c.modalScript = function () {
    spModal.confirm('${Confirmation question?}').then(function(answer) {
        if (answer === true) {
            console.log("poistoon")
        }
    });
}

## Client -> Server -> Client

1. Initialize object in client side to pass in relevant parameters to server.
2. Capture request in server side via **input**-variable.
3. Do something, and pass what is needed back to client via **data**-variable.

**Client**

    var actionObject = {
        'action': 'actionName',
        'paramter_x': parameterValue
    }

    c.server.get(actionObject).then(function(response) {
        if (response.data.actionNameResult) doSomething()
    })

**Server**

    if (input) { 
		if (input.action=='actionName') {
			// Do something
            data.actionNameResult = xxx;
		}
	} 


## Refer to specific repeat element in ng-repeat

Use variable **$index**, it doesn't need to be separately declarated.

Here an example:

**HTML**
    
    <tbody>
        <tr ng-repeat="item in c.items">
            <td>
                <input ng-change="doSomething(item, $index)">
            </td>
        </tr>
    </tbody>

In this example, **$index** will be the index of the array item used in ng-repeat. 

However, if you have multiple ng-repeats inside each other, this will not work. In this case you need to specifically state the variable used in tracking. Below an example:

**HTML**
    
    <tbody>
        <tr ng-repeat="item in c.items track by item.id">
            <td>
                <div ng-repeat="attachment in item.attachments track by attachment.id">
                    <button ng-click=c.doStuff(item.id,attachment.id)>Delete</button>
                </div>
            </td>
        </tr>
    </tbody>
