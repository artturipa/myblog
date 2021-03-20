# TDD Series, introduction
![alt text](ErikMclean_wall_e.JPG "Logo Title Text 1")

## Striving towards TDD

TDD, or Test Driven Development, is a software development discipline worth adhering to. According to TDD, development process should go as follows: 

1. Write a test that fails, immediately when test is built to the point it fails. Test should not be expanded further.
2. Write a code that enables the test succeed. When the test passes, no more code should be written.
3. Repeat until infinity.

Trying to follow TDD in ServiceNow likely won't be easy, especially if one wants to use ATF's oob test steps. Frankly, following TDD is impossible with ATF because often the test can't be constructed before there is a valid record to refer to in the test step.

However, I believe that ServiceNow developers can learn a lot from TDD. Even though TDD couldn't be followed in its strictest form, tests should be made simultaneously with the features.

## Motivation

Automated testing is required in order to enable long term flexibility with ServiceNow. Now many organizations have adopted ATF with varying level of success. What I have experienced, the most common way of adoption is to  build ATF tests after the initial development has been completed. I'm not a fan of such approach.

Building tests simultaneously with development has many benefits, for example:
* Efficiency
* Test coverage
* Fragile test problem

## Time to learn

Before I start to preach about my vision to my peers, I want to learn it myself. Hence I will try to write here my experiences following the discipline.