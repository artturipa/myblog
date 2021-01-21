# Is it right time to implement agent workspace #

Agent workspace for custom built, app engine, applications is something that I have seen requested by growing number of customers. 

ServiceNow added the ability to build custom workspaces in Orlando. Taking into account that workspaces work on a different UI framework, it's still quite a new functionality and it has its quirks. So far I have had limited experiences with it, and there are few things I wait to be improved. 

Workspaces have limited support for field types. Our team encountered this issue after building Workspace UIs to announcement and knowledge -management. Translated text -fields are essential to those processes but the field type was not yet supported. We had to build a bit messy workaround as we did not want to back down from our vision of building an application with only workspace UI for fulfillers.

Another concern I have is the look and feel of reports in dashboards. The drill down does not work out of the box, and after fixing it with some trickery suggested by ServiceNow, it still xx.

Regardless of the issues mentioned above, Workspaces are something I have waited quite long. I'm sure ServiceNow will improve the issues with coming patches and upgrades, so I wouldn't worry about them too much. Customization and building advanced features with traditional UI have been more or less extremely painful. It's nice that soon we have a state of the art frameworks to work with and build cool stuff. 

Coming back to the headline's question, is it a good time? It depends. If you are starting to build something new, I would suggest to go for Workspace regardless of the mentioned hinderances. Many of the new platform features are available only through Workspace, and you want to be able to incorporate those into your application. The case for the workspaces is only becoming more attractive as ServiceNow fixes the remaining issues.

But if on you do not have a lot of UI side development ongoing and are not yet planning to implement workspace features, it does not hurt to wait a bit longer.

For the developers, if you want workspaces and need field types not yet supported, and are not afraid of a bit messy fix, below explained how to achieve that. Please not that such structure should be removed as soon as ServiceNow provides the support for the field types. 