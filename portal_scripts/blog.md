# Useful Portal Scripts & Patterns

Here will be some useful patterns and code snippets to use in (angularJS) portal development.

I have included these scripts here foremost to help my own working. But if someone else gains something of value here, even better.

## Building Confirmation Modal
Note, this is well documented by ServiceNow, for more examples check the [reference documentation](https://developer.servicenow.com/dev.do#!/reference/api/sandiego/client/SPModal-API?navFilter=spmodal).

**HTML Link**

            <a href="javascript:void(0);" ng-click="c.modalScript(inputVar)" />

**Client Script**

    c.modalScript = function(inputVar) {

		spModal.open(
			{
				title: '${your title here}',
				message: '${your message here}',
				buttons: [
					{label:'✘ ${Cancel}', cancel: true},
					{label:'✔ ${Proceed}', primary: true}
				]
			}).then(function() {
                // Do something if proceeded
			}).then(function() {
                // Do something if cancelled
            })
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

## Interact with record producer via Macro/Widget variable

You should be able to grab g_form with 
    
    g_formInject = $scope.page.g_form

Depending on how "deep" the scope of your widget in question is, finding the g_form might not be trivial. Use this script to locate it:
 
	var g_formFound =false;
	var i = 0;
	var currentScope = $scope;
	var g_formInject;
	while (g_formFound === false && i <100) {
		i++;
		if (currentScope.page && currentScope.page.hasOwnProperty("g_form")) {
			g_formFound = true;
			g_formInject = currentScope.page.g_form;
		} else {
			currentScope = currentScope.$parent;
		}
	}
	
## Change URL parameter and reload page

This simple thing is hard to find via google. Therefore here for future use:

    // Update URL-parameter
    $location.search('parameter_name', new_value);

    // Reload page
    c.server.update().then(function() {
            $window.location.reload();
    });


## Changing first day of week of the date picker

    moment.updateLocale("en", { 
        week: { dow: 1 } // 1 = Monday
    });
   
    moment.updateLocale("fi", {  // Add other languages if needed
        week: { dow: 1 } 
    }); 

## Scroll to specific element

spUtil has method to do that in client script:

    spUtil.scrollTo("#ID_OF_HTML_ELEMENT",ANIMATION_TIME_IN_MS)

However, the element might not be present in initial load. A lazy workaround is to use timeout:

    api.controller=function(spUtil,$timeout) {
	
        function moveToInitialFocus() {
            console.log("timeback called")		
            spUtil.scrollTo("#initialfocus", 300)
        }
	
		$timeout(moveToInitialFocus, 1000)
    };

## Change order of items when in mobile

Add below class and css to containing div. Note that in case the items are separate widgets, you can add the class into portal page row in portal editor.

    @media only screen and (max-width: 767px) {  
        .reverse-class {    
            flex-direction: column-reverse!important;
        }
    }


