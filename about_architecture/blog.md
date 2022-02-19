# Architectural reflections

## Enterprise architecture

It does not get any simpler than this: In case enterprise is not aware about its operations and goals, it will not effectively. This is the problem enterprise architecture (EA) aims to solve. 

My initial impressions about EA practice were mixed as I did not not see the practicality in it. Now I have learned to appreciate it, and in this post I will discuss some undervalued EA disciplines.

## Communication

### About right level of abstraction

Domain experts have deep knowledge about the domain in question. It is often challenging to simplify solution specifications to right level of abstraction in order to communicate with a stakeholder coming from different background. We need to put effort in order to perceive the concern of another stakeholder.

I myself seek to understand the workings of a system with a great level of detail. However, time is a scarce resource. I need to stay focused and not let myself to get carried away when analysing a problem. Analysis should always be limited to the minimum necessary to solve the question at hand.

### About notation

Architecture is regurarly associated with specific notation standards. To me, it is foremost about communication. Architecture is made to address the stakeholders' concerns. 

Don't question your competency as an architect if you have not mastered notation standards. Remember that stakeholders need to understand the solution in order to make a decision. How many of your stakeholders are fluent in Archimate? Or BPMN? So don't get scared by strict notation standards. Rather aim to emphatize with your stakeholder, and try to deliver something that pleases her/his point of view.

I'm not against notation standards, they definitely have their place. If you work with enterprise having a mature EA capability with proper architecture repository, it is definitely a good idea to follow agreed notation standards to have a common language.
 
## About governance

Governance is repeatedly lacked in architectural work. I don't support a heavy governance model in places it's not needed. Still, I have seen often that a decision has been made, but lack of proper follow up causes slipping and chaos. If architectural guidelines are decided in the start of an implementation, expect them to deteriorate in case a governance model is not enforced to monitor them. Annual check might even be enough.

### About Documentation

Architectural guidelines and decisions tend to last for a long periods of time, often longer than a person stays in an occupation. 

When documentation is not properly maintained, we have no clue on why a specific architectural decison was made. And if we can't know the reasons behind a decision, we can't assess its validity.

### About Exception Handling

If you have architectural guidelines and monitoring in place, do you have a formal process to decide when an exception can be made to those guidelines? In my projects I have encountered architectural guidelines, where no-one has not been able to recognize any benefits brought by the guideline in the project, but we have still followed those because there were no process to deal with expections.