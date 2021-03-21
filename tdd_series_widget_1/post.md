# Creating a custom widget from scratch and TDD

This relates to mission I described [in the previous post](/blog/post/tdd_servicenow_intro/).

## The project

I need to create a custom widget / portal module for a customer. The plan is to develop the widget in following order:
* General layout
* Styling
* List of features as prioritised by PO
  * Load data from database
  * Edit data
  * Save data to database
  * Create new records from templates
  * Add attachments to records
  * Display additional contents in pop up
  * Move info to calendar
  * ...

## Let's start with the layout

Straight from the start I was not able to follow TDD's first rule as I started to build the layout without doing any tests. Well, no biggie.

Before finalizing the layout I got focused and started to do the UI tests. As I had already plenty of experience with ATF, I knew that finding right elements in the UI can be a pain in the a**. So I went to the widget and did some improvements in order to avoid the **fragile test problem**. 

The widget contains dynamically fetched info in a table-like form, so being able to distinguish individual elements is not trivial. Luckily after 1 min of googling I found the correct syntax to use in ng-repeat: 
>`<div class="cellContent" sn-atf-id="columnName.{{$index + 1}}">{{cellContent}}</div>`

So now I should be able test the UI by identifying specific element with the help from sn-atf-id -attribute. 

## Let's build the test

Or not... I was not able to get the "Open Portal Page" test step to function due to unkown error. It seems to pass 20% of the time, and the problem persists with different portal pages. However, with standard portal the test step works.

So before I can continue I need do debugging and fix the issue in the portal, well it's all good karma =). 

Can't care to do that at this time. Time to play Noita and continue next time.