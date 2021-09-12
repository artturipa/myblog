# Now Experience UI Components - continued

## Success

My first custom component, the resource view component, has now been completed. After some initial struggles, I was able to get to the speed with development, which turned out to be really fun.

It delights me that at last the platform gives us tools deliver superb UIs & UXs to customers. Jelly was hell. And now, working with (soon legacy) AngularJS portals feels cumbersome as well. 

## Lessons learned

### Scoping
I was building the component for a custom scoped application. Hence I thought it would be intuitive to include the component in the scope of the application scope. Problems arose.

It is possible to deploy the component into existing scope. However, it did mess up some workspace landing pages, probably due to overwriting some configuration (*sys_ux_macroponent*) records. And each time I redeployed a newer version of the component, the landing page of the workspace was erased.

I decided to abandon my idea about one scope for the app and the component. A new scope was created as instructed in the official documentation, and the component was moved there. I do not wish to encounter those problems in production.

### Configuration / Component

All good fun and games with html and css. But few things got me wondering.

Now UI custom components have React in them already after the initial scaffolding. So it is possible to do components with props à la React. I'm a bit baffled whether to continue development with React Components or HTML5 Web Components. 

This is a wonderful problem to have of course. It's great that the developers can make the choice themselves, and I'm sure that the multiple methods will prove themselves useful in different scenarios.

### Keeping things flexible

At least for now, when we are still learning to build with components, using components puts some overhead to development. It takes more time to change a statement in component's configuration than in a script include.

Therefore it is important to structure the component so that the essential settings can be changed without having to touch code of the component. For example, calculations should be done via Scripted Rest APIs & Script Includes in order to decouple those from the component. The component can then fetch the content to be displayed via API, and the content can be changed without changing the component.

Consider also defining component properties. Those can be set per component instance via UI Builder, which is of course a must when making components for common use cases. 

### To be learned

I still need to do some thinking before starting to scale up the use of components.

Now I will shift my focus to these issues:
* Deployment flow of components, especially when making changes to production
* Automated testing of components
* Moving components between instances
