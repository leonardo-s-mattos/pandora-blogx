---
layout: post
title:  "Behavior Driven Development"
date:   2020-01-06 13:50:39
categories: Engineering_playbook
---


# Play: Behavior Driven Development

## What is it:

Behavior Driven Development, or shortly BDD, is an agile software engineering technique. Before a developer starts with the implementation of a new feature the business colleagues already thought about what behavior the user really expects from the application. After thinking about it, they write it down in a Given-When-Then way and hand it over to the developer. It is very useful, if the business colleagues already hand over their feature request in the Given-When-Then style, because the developers can then directly create acceptance tests out of the requirements. The Given-When-Then formula is a template intended to guide the writing of acceptance tests for a User Story.

## When to use it:

**Working on a project, where requirements are very fuzzy:** All developers know the pain of fuzzy requirements. You are only told "Add a new button to do something" and that's it. There is so much information missing! Sure, to simple add a button can be done very quick. But we all know, that every button should do something. So, what is this button for?
Let's imagine, the business side would have handovered the requirement in the Given-When-Then way. It could have looked like this:

**Given** As a admin user I want to press on a "create user" button,  
**When** I navigate to a new screen, enter user information and press save,  
**Then** A new user is created on the database.

**Given** As a developer user I want to press on a "create user" button,  
**When** I navigate to a new screen, enter user information and press save,  
**Then** I get an error message that I don't have the right permissions.

The developer of this feature now gets a lot of more information directly from the requirements. He or she needs to think about access rights to write something on the used database. Probably, a new view for the user creation is needed. That includes some in-app-navigation. And he or she can directly use for example Gherkin to translate the requirements into test that can be automated.

The biggest benefit of teaching your business colleagues the Given-When-Then style is, that they start thinking about their requirements in a more practical way. What should the interaction of the user with the app look like and what is the expected outcome? Requirements tend to become much clearer and also a lot more precise. Unneeded UI elements can be reduced, as well as to many interaction steps (for example long navigation ways through the application).

**Starting a new project with very big requirements:** When you start a new project you tend to only have a very big vision of how your application should work in the end. E.g. Create an app for user maintenance. The first thing you need to do now is to create realistic requirements your developers can start working on. For that, you try to step into your main user persona. In our case that could be an admin with all relevant rights. What would this admin expect to see when he opens the application? A list of all existing users? Or maybe directly input options to create a new user?
By tackling your requirements in that way, you can break them down very easily. During the definition time of the requirements, Business, Product Owner and End User should communicate frequently to reduce the risk of misunderstandings.



## Expected Outcome:

Rethinking your requirements and designing them in a different way will usually lead to more granular and useful requirements with which your developers can work more easily. So over all BDD can lead to:

- More user centric requirements  
Because you always need a persona and a scenario to write down your requirements in a Given-When-Them style, you will end up with feature request that really focus on the users needs.
- More granular and precise requirements  
To really meet the Given-When-Then style requirements need to be as specific as possible. Also, while focusing on single personas, requirements end up smaller and tend to be more concrete.
- BDD reduces waist  
By handing over these super concrete, small and specific requirements your developers know what they really need to implement to fulfill the business requirements. You end up with less over production and with that, you spare waist.  
Also, you can save a lot of time regarding communication between business and development.
- Better over all Quality  
By using tools like Gherkin, developers can easily translate the Given-When-Then requirements into test cases that can even be executed automatically. Higher test coverage leads to better quality.
- Better communication between business and development  
When both sides are well trained in building up and understanding requirements in the behavior driven style, communication between these two will be much easier. Questions can be asked much more specifically and there tend to be a lot less misunderstandings about what is really wanted.



## How to use it:

### Translate your User Stories into the Given-When-Then Style

**Given** *"Persona" "Starting Point/Current Situation"*  
**When** *"Action"*  
**Then** *"Result"*


For example in case of ATM withdraw:  
**Given** my bank account is in credit, and I made no withdrawals recently,  
**When**  I attempt to withdraw an amount less than my card’s limit,  
**Then** the withdrawal should complete without errors or warnings  

**Given** my bank account is in credit, and I made no withdrawals recently,    
**When**  I attempt to withdraw an amount more than my card’s limit,    
**Then** the withdrawal should put on hold and provide me an error message  

**Given** my bank account is in credit, and I made no withdrawals recently,  
**When**  I attempt to withdraw an amount in a foreign country,  
**Then** the withdrawal should provide me a warning message of transaction cost and only complete if I confirm  

In this example the **Persona** is "I". Then the **current situation** is described. Under When the executed **actions** follow. Here "I" want to withdraw an amount of money. Followed by the described **result** of the users interaction.

Here are some tips and tricks how you can identified the needed information. Basically you need to ask yourself some questions to find out who your user is, what he or she needs to do and what he wants to achieve by performing the described action.

**Persona**:    
Who is interacting with your application?  
Are there different types of users? Admins for example?  
Do these users have different options/rights?  
How skilled are these users regarding your workflow? 

**Starting Point**:  
What does every single persona expect when starting your application?  
What information needs to be displayed before starting your workflow?  
What information might be needed regarding the connection to the result (See above example that the bank account is in credit. If the bank account would not be in credit, we would expect another result)?   
Is there an initial action to start your actual new required action (like pressing a specific button)?  

**Action**:  
What interaction does the user need to do to get his wanted result?  
What type of interaction is needed? Input? Clicks? Here we can also have more than one interaction!

**Result**:  
What is the expected outcome? A specific error message? No error? A new entry into a database?  
Try to be as concrete a possible about what you expect to be the result of the described actions.
 
### Implement Tests

There will be another Play explicitly covering how you could write test directly using the Given-When-Then style requirements in your UI5 Application using [OPA5](https://sapui5.hana.ondemand.com/#/topic/2696ab50faad458f9b4027ec2f9b884d) with [Gherkin](https://cucumber.io/docs/gherkin/reference/). ([Use OPA with Gherkin](https://sapui5.hana.ondemand.com/#/topic/45ac9f19d9414b30b121c6e00f57433c))   
 
Other tools that support this type of test development are for example: [Cucumber](https://cucumber.io/), [JBehave](https://jbehave.org/), [RSpec](https://rspec.info/)
