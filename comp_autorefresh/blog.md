# Has the custom component development gone too far?

No it has not. I love it. It's a good excuse for me to step up my javascript skills and continue towards mastery.

This was a requirement that was suprisingly hard to resolve, and that's why I feel the need to share the solution here.

## But ain't this provided by ServiceNow if you just do it right

Nope. Data resources do not cause the component contents to update even if the source data changes.

At first I thought the problem was in my configuration choices; I was calling Scripted Rest API directly from the component. The usual way to pass data into component is to use data transformation methods in the UI Builder (data resources etc). However, in this case the data fetching and analysis required some heavy lifting, and I chose to abstract that away from UI structure. 

## The solution

Nothing too fancy. Asynchronous javascript. I had troubles to pass parameters into the callback-function passed into setTimeout. The correct way was to pass the arguments directly into setTimeout function as additional arguments.

Note that the timeout needs to be defined as a property to state, because state persists between renders. And the reference to timeout function is needed, because it needs to be cancelled if user changes the state of the component.

So, do it like this:


function timeOutFunction(disptachFunction, dispatchParm1, dispatchParm2) {
    // dispatchParm1 is the name of the actionhandler to call
    // dispatchParm2 are the parameters to pass into actionhandler-function
	disptachFunction(dispatchParm1,dispatchParm2)
}


actionHandlers: {
    .
    .
    .

DATA_RECEIVED: ({ state, properties, action, updateState, dispatch }) => {
            /* Below row is needed, because if refresh happens due to user interaction, refresh should be cancelled */
            clearTimeout(state.timeOut) 
            
			updateState({
				data_for_your_component: action.payload.result,
				showLoading: false,
				timeOut:
					setTimeout(timeOutFunction, properties.timeOutDelay, dispatch,'REFRESH_DATA_ACTION_HANDLER',{
						parameter_of_interest: properties.current_value_of_parameter
					})

			})

		},
    
    .
    .
    .
}