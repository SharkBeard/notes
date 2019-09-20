# Overview
RubyCritic is a tool that wraps around other tools to provide better reporting and a letter grade for code.

# Flog
Flog reports the most tortured code in your project. http://ruby.sadi.st/Flog.html

### What it does
Flog runs an ABC check on your code. The worse a method's ABC score is, the harder it is to test the method.

### ABC
The ABC metric is how many **Assignments**, **Branches**, and method **Calls** are in your method.

* The more assignments are in your method, the more variables you have to pass in and account for in your tests.
* The more you branch in your method, the more edge cases you have to account for and the more tests you have to write to get good coverage.
* The more method calls in your method, the more you have to stub out so you are testing just the method you intend to test.

# Flay
Flay checks for structural similarities within your code. Differences in literal values, names, whitespace, and programming style are all ignored.

This helps point out what can be refactored so you only have to change something in one place and doesn't have as much repeated code.

# Reek
Reek checks the codebase for code smells. These are things that the larger Ruby community agrees are examples of poorly designed code. 

### What are Code Smells?
> One way to look at smells is with respect to principles and quality: "Smells are certain structures in the code that indicate violation of fundamental design principles and negatively impact design quality". Code smells are usually not bugs; they are not technically incorrect and do not prevent the program from functioning. Instead, they indicate weaknesses in design that may slow down development or increase the risk of bugs or failures in the future. Bad code smells can be an indicator of factors that contribute to technical debt. Robert C. Martin calls a list of code smells a "value system" for software craftsmanship.
>
> Often the deeper problem hinted at by a code smell can be uncovered when the code is subjected to a short feedback cycle, where it is refactored in small, controlled steps, and the resulting design is examined to see if there are any further code smells that in turn indicate the need for more refactoring. From the point of view of a programmer charged with performing refactoring, code smells are heuristics to indicate when to refactor, and what specific refactoring techniques to use. Thus, a code smell is a driver for refactoring.
>
> A 2015 study utilizing automated analysis for half a million source code commits and the manual examination of 9,164 commits determined to exhibit "code smells" found that:
>
> There exists empirical evidence for the consequences of "technical debt", but there exists only anecdotal evidence as to how, when, or why this occurs.
"Common wisdom suggests that urgent maintenance activities and pressure to deliver features while prioritizing time-to-market over code quality are often the causes of such smells".
There are tools, such as Checkstyle, PMD, and FindBugs for Java source code, to automatically check for certain kinds of code smells.
*[Wikipedia](https://en.wikipedia.org/wiki/Code_smell)*

### List of code smells checked
https://github.com/troessner/reek/blob/master/docs/Code-Smells.md

* [Attribute](https://github.com/troessner/reek/blob/master/docs/Attribute.md)
* [Class Variable](https://github.com/troessner/reek/blob/master/docs/Class-Variable.md)
* [Control Couple](https://github.com/troessner/reek/blob/master/docs/Control-Couple.md), including
  * [Boolean Parameter](https://github.com/troessner/reek/blob/master/docs/Boolean-Parameter.md)
  * [Control Parameter](https://github.com/troessner/reek/blob/master/docs/Control-Parameter.md)
* [Data Clump](https://github.com/troessner/reek/blob/master/docs/Data-Clump.md)
* [Duplicate Method Call](https://github.com/troessner/reek/blob/master/docs/Duplicate-Method-Call.md)
* [Instance Variable Assumption](https://github.com/troessner/reek/blob/master/docs/Instance-Variable-Assumption.md)
* [Irresponsible Module](https://github.com/troessner/reek/blob/master/docs/Irresponsible-Module.md) - Add a short, descriptive comment at the beginning of class or module to describe what it is responsible for.
* [Large Class](https://github.com/troessner/reek/blob/master/docs/Large-Class.md), including
  * [Too Many Constants](https://github.com/troessner/reek/blob/master/docs/Too-Many-Constants.md)
  * [Too Many Instance Variables](https://github.com/troessner/reek/blob/master/docs/Too-Many-Instance-Variables.md)
  * [Too Many Methods](https://github.com/troessner/reek/blob/master/docs/Too-Many-Methods.md)
* [Long Parameter List](https://github.com/troessner/reek/blob/master/docs/Long-Parameter-List.md), and its special case [Long Yield List](https://github.com/troessner/reek/blob/master/docs/Long-Yield-List.md)
* Low Cohesion, including
  * [Feature Envy](https://github.com/troessner/reek/blob/master/docs/Feature-Envy.md)
  * [Utility Function](https://github.com/troessner/reek/blob/master/docs/Utility-Function.md)
* [Module Initialize](https://github.com/troessner/reek/blob/master/docs/Module-Initialize.md)
* [Nested Iterators](https://github.com/troessner/reek/blob/master/docs/Nested-Iterators.md)
* [Missing Safe Method](https://github.com/troessner/reek/blob/master/docs/Missing-Safe-Method.md), formerly known as Prima Donna Method - If you have an `update!` method make sure you also have an `update`
* [Simulated Polymorphism](https://github.com/troessner/reek/blob/master/docs/Simulated-Polymorphism.md), including
  * [Manual Dispatch](https://github.com/troessner/reek/blob/master/docs/Manual-Dispatch.md) - Don't check if method exists before you call it. 
  * [Nil Check](https://github.com/troessner/reek/blob/master/docs/Nil-Check.md) ([Tell, Don't ask](http://robots.thoughtbot.com/tell-dont-ask)) - Should probably be using more OOP or Polymorphism
  * [Repeated Conditional](https://github.com/troessner/reek/blob/master/docs/Repeated-Conditional.md) - Don't check the same thing repeatedly
* [Subclassed From Core Class](https://github.com/troessner/reek/blob/master/docs/Subclassed-From-Core-Class.md) - Don't subclass from built-in Ruby classes
* [Too Many Statements](https://github.com/troessner/reek/blob/master/docs/Too-Many-Statements.md)
* [Uncommunicative Name](https://github.com/troessner/reek/blob/master/docs/Uncommunicative-Name.md), including
  * [Uncommunicative Method Name](https://github.com/troessner/reek/blob/master/docs/Uncommunicative-Method-Name.md) e.g. `x()`, `i()`, `item1()`, `snakeCase()` 
  * [Uncommunicative Module Name](https://github.com/troessner/reek/blob/master/docs/Uncommunicative-Module-Name.md) e.g. `X`, `I`, `Item1`
  * [Uncommunicative Parameter Name](https://github.com/troessner/reek/blob/master/docs/Uncommunicative-Parameter-Name.md) e.g. `x`, `i`, `item1`, `snakeCase`
  * [Uncommunicative Variable Name](https://github.com/troessner/reek/blob/master/docs/Uncommunicative-Variable-Name.md) e.g. `x`, `i`, `item1`, `snakeCase`
* [Unused Parameters](https://github.com/troessner/reek/blob/master/docs/Unused-Parameters.md)
* [Unused Private Method](https://github.com/troessner/reek/blob/master/docs/Unused-Private-Method.md)
