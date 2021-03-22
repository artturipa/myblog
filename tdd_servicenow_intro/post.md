# TDD Series, introduction
![pic](https://source.unsplash.com/81rOS-jYoJ8/800x500)

## Striving towards TDD

TDD, or Test Driven Development, is a software development discipline worth adhering to. According to TDD, development process should go as follows: 

1. Write a test that fails. No more testing logic should be written that is required for the test to fail.
2. Write a code that allows the test to pass. No more code should be written that is required for the test to pass.
3. Repeat until infinity.

I have a feeling that trying to follow TDD in ServiceNow won't be easy, especially if I will use ATF's out-of-the-box test steps. Frankly, following TDD with ATF is impossible, because often the mandatory references in tests can't be constructed before a configuration record has been created.

However, I believe that ServiceNow developers can learn a lot from TDD. Even though TDD couldn't be followed in its strictest form, tests should be made simultaneously with the features.

## Motivation

Automated testing allows ServiceNow to stay flexible while building custom application and configurations. Without automated testing risks grow and manual testing starts to considerable (=huge) amount of time. I have seen many organizations adopt ATF with varying level of success. Usually ATF tests are built after the initial development has been completed. I'm not a fan of such approach.

Building tests simultaneously with development has many benefits, for example:
* Tests are actually done
* Configurations will be testable
* Efficiency in building the tests
* Higher test coverage
* Tests are less prone to fragile test problem

## Time to learn

Before I start to preach about my vision to my peers, I want to learn the discipline myself. Hence I will be posting about my initial experiences with the journey. 

Rock on.