#Architectural reflections

##Importance of enterprise architecture

It does not get any simpler than this: In case enterprise is not aware about its operations and goals, it will not effectively. This is the problem enterprise architecture (EA) aims to solve. 

My initial impressions about EA practice were mixed because I did not understand its practicality. Now I have come to appreciate it, and in this post I will discuss some EA disciplines I feel are lacking .

##Communication

###About right level of abstraction

Domain experts have deep knowledge about the domain in question. It is often challenging to simplify the specifications of a solution to a right level of abstraction to a stakeholder with a different background. 

It is a rare case where encryption expert is able to select correct level of detail when discussing security issues with management. This happens when one is not able to perceive the concern of another stakeholder.

I myself am a such a person that delights about understanding the workings of a system with a great level of detail. However, the time is scarce resource, I need to stay focused and not allow myself to get carried away. **Analysis should always be limited to the minimum necessary to solve the question at hand**.

###About notation

Architecture is regurarly associated with specific notation standards. To me, it is foremost about communication. Architecture is made to address the stakeholder concerns. Stakeholders need to understand the soluiton in order to make a decision. How many of your stakeholders are fluent in Archimate? Or BPMN? So don't get scared by strict notation standards you might have seen. Rather emphatize with your stakeholder, and try to deliver something that pleases her/his point of view.

I'm not against notation standards, they definitely have their place. If you are working with enterprise having a mature EA practice and governed architecture repository, it is definitely a good idea to follow agreed notation standards as a common language.
 
##About governance

Governance is repeatedly lacked in architectural work. I don't support a heavy governance model to places it's not needed. Still, I have seen often that a decision has been made, but lack of proper follow up causes slipping and chaos. If architectural guidelines are decided in the start of an implementation, expect them to deteriorate in case a governance model is not enforced to monitor them. Annual check might even be enough.

###About Documentation

Architectural guidelines and decisions tend to last for a long periods of time, often longer than a person stays in an occupation. 

When documentation is not properly maintained, we have no clue on why a specific architectural decison was made. And if we can't know the reasons behind a decision, we can't assess its validity.

###About Poikkeuksien hyväksyminen

If you have architectural guidelines and monitoring in place, do you have a formal process to decide when an exception can be made to those guidelines? In my projects I have encountered architectural guidelines, where no-one has not been able to recognize any benefits brought by the guideline in the project, but we have still followed those because there were no process to deal with expections.



##About identifying vaikutuksia muualle

One key asset of a good architect is to be able to identify x implications to other systems and processes. 

 

All solutions exists in a context, and it is not merely enought that a team focuses building its own solution. 

* What will happen to process specific application when implementing one ESM platform

* What will happen to integrity of AD Master data if data is enriched in a downstream application 

* What will (should) happen in enterprise's recruitment strategy when