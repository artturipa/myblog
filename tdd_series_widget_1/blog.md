# Creating a custom widget from scratch and TDD

This relates to mission I described [in the previous post](/blog/post/tdd_servicenow_intro/).

## The project

I will be creating a custom widget / portal module for a customer. The plan is to develop the widget in following order:
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

Straight from the start I was not able to follow TDD's first rule to start with tests. Instead I went straight to building the html layout. Well, no biggie.

Before finalizing the layout, I got focused and went for the UI tests. Having plenty of experience with ATF, I knew that finding right elements in the UI can be a pain in the a**. So I went back to the widget, and did some improvements in order to make the test more robust. 

The widget contains dynamically fetched content in a table-like form, and I want to be able to distinguish individual elements in the table. Luckily after 1 min of googling I found the correct syntax to use in angular's ng-repeat: 
>`<div class="cellContent" sn-atf-id="columnName.{{$index + 1}}">{{cellContent}}</div>`

Now I should be able to build the UI tests by identifying specific element with **sn-atf-id** -attribute. 

## Let's build the test

Or not... I was not able to get the "Open Portal Page" test step to function due to unkown error. It seems to pass 20% of the time, and the problem persists with different portal pages. However, with standard portal the test step works just as expected.

So before I can continue I need do some debugging to locate and fix the issue in the portal, well it's all good karma =). 

Can't care to do that at this time. Time to play Noita and continue next time.