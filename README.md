##_Summary of the Clean Code by Robert Cecil Martin_


#1. TABLE OF CONTENTS
- [1. TABLE OF CONTENTS](#1-table-of-contents)
- [2. MEANINGFUL NAMES](#2-meaningful-names)
- [3. CREATING FUNCTIONS](#3-creating-functions)
  - [1. FUNCTIONS](#1-functions)
  - [2. FUNCTION ARGUMENTS](#2-function-arguments)
  - [3. VERBS AND KEYWORD](#3-verbs_and_keywords)
  - [4. COMMAND QUERY SEPERATION](#4-command-query-seperation)
  - [5. DONT DUPLICATE CODE](#5-dont-duplicate-code)
  - [6. HOW TO WRITE FUNCTIONS LIKE THIS](#6-how-to-write-functions-like-this)
- [4. COMMENTS](#4-comments)
- [5. FORMATTING MATTERS](#5-formatting-matters)
  - [1. FORMATTING](#1-formatting)
  - [2. VERTICAL FORMATTING](#2-vertical-formatting)
  - [3. HORIZONTAL FORMATTING](#3-horizontal-formatting)
- [6. ERROR HANDLING](#6-error-handling)
  - [1. CHECKED EXCEPTIONS](#1-checked-exceptions)
  - [2. CONTEXT WITH EXCEPTIONS](#2-context-with-exceptions)
  - [3. DEFINE EXCEPTIONS IN TERMS OF HOW THEY ARE CAUGHT](#3-define-exceptions-in-terms-of-how-they-were-caught)
  - [4. SPECIAL CASE PATTERN](#4-special-case-pattern)
  - [5. DONT RETURN NULL](#5-dont-return-null)
  - [6. DONT PASS NULL](#6-dont-pass-null)
- [7. INTEGRATING WITH THIRD PARTY LIBRARIES](#7-integrating-with-third-party-libraries)
  - [1. USE THIRD PARTY CODE](#1-use-third-party-code)
  - [2. EXPLORING AND LEARING BOUNDRIES](#2-exploring-and-learing-boundries)
  - [3. LEARNING TESTS ARE BETTER THAN FREE](#3-learing-tests-are-better-than-free)
  - [4. USE CODE THAT DOES NOT EXIST YET](#4-user-code-that-does-not-exist-yet)
  - [5. CLEAN BOUNDARIES](#5-clean-boundaries)
- [8. WRITING UNIT TESTS](#8-writing-unit-tests)
  - [1. THREE LAWS OF TDD](#1-three-laws-of-tdd)
  - [2. KEEP TESTS CLEAN](#2-keep-tests-clean)
  - [3. TESTS ENABLE THE -ILITIES](#3-tests-enable-the--ilities)
  - [4. CLEAN TESTS](#4-clean-tests)
  - [5. BUILD-OPERATE-CHECK PATTURN](#5-build-operate-check-pattern)
  - [6. DOMAIN SPECIFIC TESTING LANGUAGE](#6-domain-specific-testing-language)
  - [7. DOUBLE STANDARD?](#7-double-standard?)
  - [8. ONE ASSERT PER TEST](#8-one-assert-per-test)
  - [9. SINGLE CONCEPT PER TEST](#9-single-concept-per-test)
  - [10. FIRST](#10-first)
  - [11. IMPORTANCE](#11-importance)
- [9. WRITE CLASSES THE RIGHT WAY](#9-write-classes-the-right-way)
- [10. BUILD MAINTAINABLE SYSTEMS](#10-build-maintainable-systems)
  
  

#2. MEANINGFUL NAMES

“If a name requires a comment, then the name does not reveal its intent”

* Write explicit code – naming variables and methods can reveal the entire intent of the code
* Avoid using words that would be confusing like “List” as they refer to programming types and could be misleading : accountList should be accounts
* Avoid using characters that look like numbers i and L or capital o
* disinformative vs noninformative
* noise words “data” “info” – noninformative
* Types should almost never be in a name “table” “string” “object”
* Names should be distinguished so a user can look at them and understand the differences
* Use pronounceable names
* Use searcheable names – longer names trump shorter names
* Author’s pref – single letter names should only be used as local variables inside small methods – length of the name should correspond to the size of its scope
* Avoid encoding names
* Avoid Hungarian Notation with typing as part of the variable name – simply not needed nowadays
* Stop prefixing member (instance) variables with m_ or _
* Decorating Interfaces vs Classes with a prefix / suffix – opinion – he prefers
* ClassImp or vs IType
* Don’t force someone to map variable names in their mind – n = username…smart programmer vs professional programmer – clarity is king
* Class names should be nouns – English 101 – NOT VERBS
* Method names should be verbs
* Use get, set, is – javabean standard
* When constructors are overloaded, use static factory methods with explicit names – liked this one, possibly make the constructors private
* Don’t get cute with naming by means of jokes (inside or well known)
* Use consistent naming – Get, Set, Controller – makes it easier to understand and code various parts of an application
* Avoid puns – add for a collection vs add for setting a value – two different meanings with the same name
* Use technical names such as pattern names or CS terms in your names – other programmers will understand them better than the problem domain in some cases
* Fall back to the problem domain for a name if there is no suitable technical name
* Adding context to naming can clarify their use – prefixes can work but putting variables into classes may work out better

“Hardest thing about choosing good names is that it requires good descriptive skills and a shared cultural background”

Renaming things that don’t make sense as you work in code is a good thing.

#3. CREATING FUNCTIONS
##1. Functions
* 1st rule – Functions should be small
* 2nd rule – Functions should be smaller than that!
* Functions should barely be 20 lines long…
* Each function should lead you to the next function in a compelling order – like telling a story
* They should do ONE thing
* Code within if’s or block statements should be one line long, meaning they should call another function…overkill?
* The indent levels of a function probably shouldn’t be more than two tabs! (tabs vs spaces)
* Prepend “TO” to the name of your function and see if you can describe what it should be doing…it may seem like more than one thing
* “Another way to know that a function is doing more than one thing is if you can extract another function from it with a name that is not a restatement of it’s implementation”
* Functions that do just one thing can’t be divided into sections…they’re not long enough
* Keep functionality at the same level of abstraction – interesting…“getHtml()” vs “getPath” vs path.append(“newline”)
* The StepDown Rule – the code should read like a paragraph of “To do …” – and those should be at the same basic level of abstraction
* Switch statements – should be created only once and should be used to create polymorphic objects – objects with the same methods but different implementations
* Use descriptive names – Ward’s Principle “you know you’re working on clean code when each routine turns out to be pretty much what you expected”
* The ugliest functions I “write” are refactors – they take too many arguments, because the code isn’t separated by concern – mixing data gathering, logic and presentation!
* The smaller and more focused a function, the easier it is to name
* Don’t be afraid to make a long name – a long descriptive name is better than a short enigmatic one
* A long name is better than a long comment
* Be consistent in your naming – again, it should be like reading a paragraph – easy to follow

##2. Function Arguments
* You should basically never use more than 2 arguments in a function – if so, there’d better be a great reason
* You do this by making values instance variables and then use the instance methods to work with those arguments
* Testing with multiple arguments becomes very difficult
* Niladic – no arguments – absolute best case
* Monadic – single argument – asking a question about the argument, or transforming and returning
* Other monadic uses are events
* output variables can be confusing and probably avoided where possible
* Immediately tells you that the function is going to do something different based on the value of the flag
* Dyadic Functions – harder to understand just by looking at them…easy to mix up the order of the params
* Triadic functions – significantly harder than dyadic – avoid if possible – make arguments class members so niladic methods could be called
* If a method needs more than 2 or 3 arguments, pass in an object
* When using argument lists, still stick to the same rule – no more than 3 – the list of objects would be your third…n parameter

##3. Verbs and Keywords
* Naming your functions with good verbs and using the arguments as keywords can be a good thing assertExpectedEqualsActual(expected, actual);
* Your functions should not have side-effects – if it says it does one thing, it should ONLY do that thing
* Avoid making methods that require you to inspect the declaration – that means the method isn’t named something that identifies its true intention well
* Generally speaking, output variables should be avoided

##4. Command Query Separation
* Functions should do something or answer something, not both
* Prefer exceptions as opposed to error codes
* Extract the try/catches out into functions that do the body of work – Throw liberally, catch sparingly
* Error handling is “one thing” – so it should be the beginning and end of your function

##5. Don’t Duplicate Code
* One of the biggest problems in programming – duplication leads to multiple places to change and more places where bugs can occur
* Don’t necessarily stick to the single entry / single exit rule – just make sure the functions are small enough to understand

##6. How do you make functions like this?
* Revise revise revise. Write your code first and start chopping away at it until you have something that follows the rules mentioned

#4 COMMENTS
* “At best, comments are a necessary evil”
* “The purpose of a comment is to compensate for our failure to express ourself in code”
* Try to express yourself in code rather than a comment
* Comments should be updated as code is updated, but a better use of time would be to make the code itself more expressive
* Inaccurate comments are worse than no comments at all – they’re lies…misleading
* Comments do NOT make up for bad code
* If you feel you need to comment the code, it might be a good time to assess whether you should create a new method that will better express what you’re attempting to do
* “The only good comment is the one you found a way not to write”
* Copyright and licensing are good uses of comments – they’re usually required
* These comments should provide a reference to the full body of the license rather than including the text in the comment
* Another good use shown in the book is showing the expected format of a regular expression
* Clarifying comment to describe what you’re doing when working with a third party library you cannot change is also useful at times – this can be tricky because you could make bad assumptions and misinform – so take caution
* TODO – sometimes ok, but don’t want them to litter up your repo
* Documentation for public API’s – just be careful not to write non-truths here as it’s easy to do if you don’t update your comments as the code changes
* Most comments are just bad comments…not needed and code should have been changed
* Took some shots at Javadocs for Tomcat – they were admittedly pretty useless
* Too easy to write misleading comments – subtle differences can lead people down the wrong path
* Author generally dislikes commenting of methods – for the fact that they will eventually become misleading if not so at the outset
* Log journals – used to be useful before source control – now they should be removed – SQL anyone?!
* Noise – useless, add nothing comments – restating the obvious
* Comments that complain about things are bad – they should be refactored into useful methods
* Don’t use a comment when you can use a function or variable
* Banners – used to identify a section in code – can be useful but also lose effectiveness if overused
* Don’t put your bylines in the code- let the source control keep track of that for you
* Do NOT comment out code…delete it – source control will provide you a history
* HTML Comments in your code should NOT be used…it’s unreadable
* Only comment on the code right next to the comment – do not make system type of comments as they can quickly become incorrect
* Don’t write too much information in a comment
* The comment should be easy to connect to the code it’s describing – if it doesn’t then the comment is worse than useless
* Function headers – a well named function is better than a comment header
* Only use Javadocs (or similar) for public API’s – they do more harm than good in private repos

#5. FORMATTING MATTERS
##1. Formatting
* If your code is a mess, then people will assume that your attention to detail in how the app was coded is also a mess – perception
* Teams should adopt formatting rules and follow them
* Automated tools help with the process
* “Code formatting is important”
* Code formatting has a direct affect on maintainability and extensibility of code over time

##2. Vertical Formatting
* Try to keep max length around 500 lines long and smaller is better – FitNesse app is in this range
* Tomcat and Ant – several thousand lines long and at least half are over 200
* Newspaper metaphor – read it vertically – headlines at the top detail increases as we go down the page
* Separate concepts with blank lines
* Closely associated code should be grouped together so it’s dense
* Concepts (methods) that are closely related should be grouped as closely together as possible to keep from hunting through files
* Variable declarations should be as close to their usage as possible
* If the methods are short, then the variable declarations should be at the top of the function!
* Control variables for loop should be defined within the loop
* Instance variables should be declared at the top of a class
* When one function calls another, those should be close vertically in the file
* Conceptual affinity – when methods do similar things or are named similarly, they should also appear close to each other
* Vertical ordering of methods – the caller should be first, then the callee, and that method’s callee, etc…on down the page

##3. Horizontal Formatting
* How wide should a line be?!
* In the popular projects examined, it appeared that 40% of lines were between 20 and 60 characters
* Another 30% of lines were less than 10 characters…
* Author suggests that beyond 100-120 is careless
* Put spaces on both sides of an assignment operator (equals sign)
* Don’t put spaces between the function name and the parens
* DO put spaces after individual arguments / parameters in a list – shows they are separate
* Also use spacing to indicate the precedence of operations – think of spacing in math equations with several parentheses – author calls it out for order of precedence, I actually don’t like this one – I prefer grouping with parens
* Lining up variable declarations, names, types – found that it was distracting to the “story” of the code….I agree
* Hierarchically lining up code based on it’s scope – super important
* Author would sometimes condense multiple lines into one (like a get; set;) eventually set it back for readability (breaking indentation)
* What about for PRINT statements in SQL???
* while statements – indent the semicolon on the next line…otherwise they’re hidden
* Follow the team’s formatting rules…don’t go vigilante

#6. ERROR HANDLING
* This chapter was written by Michael Feathers, known for “Working Effectively with Legacy Code” http://amzn.to/2hWUVtt
* Error handling is important and needed, but if it obscures logic, it’s being done wrong
* Use Exceptions rather than Return Codes
* Return codes force the caller to check the codes and act accordingly, which obscures logic
* Throwing an exception is cleaner as the logic isn’t obscured by the error handling
* Keeps the logic away from the errors – separation of concerns
* Error handing and Go – https://blog.golang.org/error-handling-and-go
* Start with your try catch finally statements
* Doing so forces you to think about the state of your application – you should be left in a good state if there is an error and that would resume in the catch
* Try to write tests that FORCE exceptions
* Then add behaviors to your handler to handle the exceptions
* This helps you maintain the scope of your try/catch’s

##1. Checked Exceptions
* A thing in Java that would force a developer to list all the types of exceptions that could be returned from a called method
* Violates the open/closed principle
* Every method between the method being called and the calling method would have to include those exception lists. If you change what the called method can throw, you need to revisit every single method
* Typically the costs / maintenance outweigh the benefits

##2. Context with Exceptions
* Provide enough context with your exception to determine the source and location of the error – No more “Null Reference”
* Stack trace isn’t enough – doesn’t identify the intention
* Include messages along with the exceptions to help identify what the intention was, along with any stack / location info

##3. Define Exceptions in terms of How they are Caught
* Think in terms of how the exception will be used
* Don’t create redundant exception classes if they’ll simply be used to do the same thing, such as logging the error
* Think in terms of actionable exceptions
* In the case of utilizing another libraries exceptions, if you’ll be doing the same thing for each type, write your own wrapper to simplify / reduce copies
* Wrapping 3rd party API’s are a “best practice” according to the book

##4. Special Case Pattern
* Martin Fowler’s Special Case pattern
* Visual Studio magazine’s take on The Special Case Pattern
* The Null Object pattern
* Don’t use catch’s to handle additional business logic flow
* The book uses the notion of a meal expense. Get the meals.getTotal() catch that error if it didn’t exist and then add perdiem
* So, rather than return the expenses, return a MealExpense object that has a getTotal() method – if there were meals, then the MealExpense object getTotal will total the meals cost, otherwise it’ll return a PerDiemMealExpense that extends MealExpense

##6. Don’t Return NULL
* Says to use the Special Case Pattern – I think we’ve referred to it as the NULL object pattern?
* NULL checks junk up your code and deter from the algorithm / application logic
* If not doing a special case pattern, consider throwing an exception rather than returning null
* If dealing with a 3rd party that returns nulls, consider the facade pattern and intercept and return an object
* Poetry reading of Michael’s favorite poem: http://www.codingblocks.net/podcast/episode-10-csharp-6-and-roslyn/

##7. Don’t Pass NULL
* Worse than returning null!
* Just don’t allow methods to take in null parameters – will make your code much cleaner / more maintainable

#7. INTEGRATING WITH THIRD PARY LIBRARIES
##1. Using Third-Party Code
“There is a natural tension between the provider of an interface and the user of an interface”
* Provider strives for broad applicability, users have a specific need
* Advise passing around an abstraction around your system…avoid returning it from, or accepting it as an argument to public API

##2. Exploring and Learning Boundries
* How do you start integrating a new 3p?
* Not our job to test the 3p
* Argue it’s in our best interest to write tests
* Keep the tests to validate functionality after upgrade
* Spending a day or two reading documentation to integrade a 3p? Definitely written in the days before “require()”
  *  Call these “learning tests”

##3. Learning Tests are Better than Free
* The tests are “free”, you’d be doing the work anyway – and you have them around for smoke tests and future migrations
* With boundary tests, you’ll know when the 3p library changes in an incompatible way
* Without boundary, you might be tempted to not update 3p dependencies as often

##4. Using Code that does not exist Yet
* Abstractions help work around code that hasn’t been written yet (Adapter pattern)
* Protects you from future changes
* Provides a convenient seam for testing

##5. Clean Boundaries
* Code at the boundaries needs clear separations and tests that define the expectations
* We should limit our code’s dependencies on the boundaries using Wrappers and Adapters
* As Joe likes to say, push the weird stuff to the edges of our code
* Question: When do you wrap, and when do you adapt?
  * https://en.wikipedia.org/wiki/Adapter_pattern
  
#8. WRITING UNIT TESTS
##1. Three laws of TDD
* You may not write production code until you have written a failing unit test
* You may not write more of a unit test than is sufficient to fail, and compiling is failing
* You may not write more production code than is sufficient to pass the currently failing test

##2. Keeping Tests Clean
* Problem with this approach – test code could outgrow your prod code and become unmanageable
* Is dirty test code better than no test code?
* Tests must change as the production code changes
* The dirtier the tests, the harder they are to change
* Tests can become a liability due to technical debt of the dirtiness
* Abandoning test code has the following consequences
* Production code defects rise
* Fear of changing code increases
* Cleaning / refactoring code descreases due to lack of confidence (Code rot!!!)
* Test code is as important as production code – it should be treated as a first class citizen and should be as clean as production code.

##3. Tests Enable the -ilities
* Tests are what keep your production code flexible, maintainable and reusable.
* Tests allow you to make changes to code without fear.
* Tests enable change.
* Tests enable improving architecture.
* Without tests, your code base rots.

##4. Clean Tests
* Readability
* More important in Unit Tests than in production code?
* Clarity
* Simplicity
* Density of expression
* Much like writing great functions, if you have to learn a ton of details to make heads or tails of a test, it can be improved.

##5. Build – Operate – Check Pattern
* Build – builds up the test data
* Operate – works on the test data
* Check – ensure the operation yielded the expected results

##6. Domain Specific Testing Language
* Tests are written in specific ways for various testing platforms
* Helps readability

##7. Double Standard?
* Interesting points made on asserts in line with values…
* Author chose to do upper / lower combination of characters in an initialism to indicate whether the particular test result should have been true or false
* Unit tests are often not held to the same standard in terms of performance

##8. One assert per test
* Makes tests very easy to read
* Given, When, Then naming
* Author actually prefers multiple asserts in some scenarios (XML example from book)
* Author notes that single assert is a good guideline
* Should try to minimize the number of asserts

##9. Single concept per test
* More important than a single assert per test
* Ensures that your tests are laser focused and not testing miscellaenous (non-related) things

##10. FIRST
* (F)ast – tests should be fast / run quickly
* (I)ndependent – tests should NOT depend on each other – tests should be able to be run in any order they like
* (R)epeatable – they should be repeatable in ANY environment without need for any specific infrastructure
* (S)elf-validating – they should have a boolean output – pass or fail, nothing else
* (T)imely – they need to be written in a timely fashion – just before the production code is written – ensures they are easy to code against

##11. Importance
* Unit Tests are as important if not moreso than the production code they’re for becasue they allow you to make changes confidently and without fear. They allow you to mold your code over time to improve flexibility / maintainability.

#9. WRITE CLASSES THE RIGHT WAY 
* https://www.codingblocks.net/podcast/how-to-write-classes-the-right-way/

#10. BUILD MAINTAINABLE SYSTEMS
* https://www.codingblocks.net/podcast/how-to-build-maintainable-systems/
