---
layout: post
title:  "Refactoring"
date:   2020-01-09 13:50:39
categories: Engineering_Playbook
---

# Play: Refactoring

## What is it?

Refactoring describes the process of reworking your code without changing any of the existing functionality. Your goal is to improve the quality of your code regarding readability, performance, maintainability and extendability. 

## When to use it?

Before you start working on code, you should always understand what this code is doing!
Especially, if it is not your own code you are going to touch, take the time to read through everything, debug a little bit and discover what is going on.  
Please never ever try to refactor code you do not understand. The chance that you destroy something you haven't been aware of is very high!

### Tests, Tests and more Tests 

The biggest fear you should face when touching code, independent of if you only want to refactor it or add new functionality, is the fear of breaking something! Especially if you are working on a bigger project containing multiple classes and countless objects, you'll never know how these are all related to each other. Even if you developed them all by yourself, the chance that you'll remember every single connection will be lowered down with every new class or object added.  
That is why you should never ever start refactoring code that is not well tested!  
But what does this "tested" mean in the context of refactoring?  
It does **not** mean that twenty different colleagues clicked through your application and checked if everything worked as expected. In this context, tested means that you have some written test in place. These test can be on different testing pyramid levels and can be written with multiple different frameworks. But most important to secure stable functionality are basically unit tests.  

So, when are you "*allowed*" to start refactoring your code? 
You can start refactoring, when at least the code part you want to touch is well covered with unit or regression tests. Well covered means, that by executing the existing test you can be sure that the touched code kept its existing functionality. If not, the test would have failed.  
You'll sometimes discover, that code you need to work on is not tested enough or at all. Then please take the time and write some small test first! 


**Messy code with no structure:** Facing code you are not able to understand easily because it is written in a very messy and unstructured way is a very common issue for developers. Developers who are really into developing complex algorithms, or in a coding flow in general, do not care how that stupid variable is named or if the parameter got a comprehensible name. That's why cleaning up the code definitely makes sense. Check, if the tests are in place, and then start renaming variables, parameters, functions, objects or whatever pops up. Restructure the class hierarchy and/or extract inline functions to higher the readability.  
The general advice for cleaning up code is to stay with the clean code rules defined for the used programming language or defined by your team.

**Badly maintained legacy code:** In general, legacy code is a description for old, messy, unmaintained code. This also includes only very low or no test coverage at all. Regarding what you learned at the beginning of this play, this would mean you are not allowed to refactor this code until you wrote some tests. The biggest issue with legacy code is, that depending on the technology, it tends to be written in a way where testing is hard, if not even impossible.  
So what now? You are not allowed to refactor, because there are no test to secure that you don't destroy anything. But you would first need to refactor the code, to make it testable.  
I Know, this sounds like a worst case scenario and it actually is!   
The recommended solution is to build some characterization test, to be as safe as possible that you at least do not destroy the original behavior of your software during refactoring. A characterization test is a test, that does not test functionality on a unit level, but test actual interaction with your application as an example. Typical black-box testing. After implementing some of these tests you start with refactoring the code to make it testable. You write some tests. You refactor only few lines of code again and so on. Try to keep these cycles short and touch as few lines of code at once as possible.

But why should you touch legacy code at all, if refactoring is so much effort? Mostly, legacy code needs to be refactored, because it was not designed in an extendable way. But new requirements pop up and extensions are now badly needed. Another scenario could be, that some of the legacy code functionality should be integrated into another project, which is designed differently. For example, the new project is designed object-oriented during our legacy code is build in a functional way. Then we need to refactor the legacy code, so that we can extract the functionality we want to migrate into the other project.

**Working on code with performance issues:** Sometimes, code may not even look bad at the first look. But then you trigger a performance test and everybody starts crying right away. Seconds, maybe even minutes, of loading circles spinning their rounds. Or even worse, empty screens with nothing displayed, because the backend is working in the background.  
To work on performance issues you definitely need to have some performance test in place, so that you can measure your refactoring progress. Besides that, the general rules for refactoring apply. You should better have a test in place for every line of code you touch! Because, also performance improvements can break some other existing logic. 


## Expected Outcome 

- Higher over all code quality  
By investing some effort in cleaning up your code you will discover minor or even bigger issues inside your code. By following the boy scout rule (Always leave the camp side cleaner as you found it) your code quality will rise over time
- Better readability  
When you start renaming variables, parameters and functions your code will become more readable for other developers
- Better maintainability  
By improving the quality and the readability your code will also be easier to maintain. Especially if you are not fixing stuff by yourself, but others need to clean up your stuff ;-)
- Better performance  
Restructuring functions by removing inline declarations, reducing loops or refactor especially with the goal of archiving a better performance will make your code perform quicker on a longer run

## How to use it?

Let's have a look into a very simple JavaScript code example.  
Obviously, this is a function. Do you initially know the returned result of the `doALotOfStuff` function?


```
function doALotOfStuff (a, b, c) {
    a.forEach(function(i){
	this.calc = function (b, c, i) {
		var result = b + c + i;
		console.log(result);
	}(b, c, i);
    })
}

doALotOfStuff([1,2,3], 5, 6);
```

Let's refactor the naming to make it easier to read:

```
function doALotOfStuff (aNumbers, iOne, iTwo) {
    aNumbers.forEach(function(iCurrentValue){
	this.calc = function (iFirst, iSecond, iThird) {
		var result = iFirst + iSecond + iThird;
		console.log(result);
	}(iOne, iTwo, iCurrentValue);
    })
}

doALotOfStuff([1,2,3], 5, 6);
```

By giving each used parameter an own name it is easier to understand, that we are using different values here. To name the parameter of two different functions the same could lead to the conclusion, that they have the same value. That's not the case in this example.  
What do you think regarding performance? Is this a clean code example or do you still discover some room for improvements?  
In JavaScipt `forEach` indicates a loop. That means, `calc` is newly defined in every loop step. That's not really clean.

```
function doALotOfStuff (aNumbers, iOne, iTwo) {
    aNumbers.forEach(function(iCurrentValue){
        calc(iOne, iTwo, iCurrentValue);
    })
}

function calc (iFirst, iSecond, iThird) {
    var result = iFirst + iSecond + iThird;
    console.log(result);
}

doALotOfStuff([1,2,3], 5, 6);
```
We now extracted the inline function `calc` into an own function. That leads to two benefits: Tthe function is not defined over and over again and debugging would also be much easier.
