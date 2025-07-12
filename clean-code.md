# Clean Code by Robert C. Martin (Uncle Bob)

## Clean Code
- it's not only coding - it's called "maintenance"

- 5S principles - Japan's set of disciplines

  - Seiri - organization - sutable naming
  - Seiton - tidiness - "A place for everything and everything in its place"
  - Seiso - cleaning - keep the workplace free of wires, comments ext.
  - seiketsu - standardization - the group agrees about how to keep the workplace clean
  - shutsuke - final - self-discipline - follow the team practices

- "A stitch in time saves nine. The early bird catches the worm. Don’t put off until tomorrow what you can do today"

- The small things matter over the time

- An advocate of thinking of the architectural approaches rooted in deep domain knowledge and software usability

- And while rework in the manufacturing metaphor leads to cost, rework in design leads to value.

- Abstraction is evil. Code is anti-evil, and clean code is perhaps divine

- There are two parts to learning craftsmanship: knowledge and work. You must gain
  the knowledge of principles, patterns, practices, and heuristics that a craftsman knows, and
  you must also grind that knowledge into your fingers, eyes, and gut by working hard and
  practicing.

- LeBlanc’s law: Later equals never

- Keeping your code clean is not just cost effective; it’s a matter of professional survival.

- So too it is unprofessional for programmers to bend to the will of managers who don’t
  understand the risks of making messes. (it is my responsibility to be professional and sync with the manager)

- Conundrum - You will not make the deadline by making the mess. Indeed, the mess will slow you down instantly, and will force you to miss the deadline.

- "Code-sence" - with so many refactoring and experience?

- Bad code tries to do too much, it has muddled intent and ambiguity of purpose. Clean code is focused

- "crisp abstraction" - Despite this seeming juxtaposition of meaning, the words
  carry a powerful message. Our code should be matter-of-fact as opposed to speculative.
  It should contain only what is necessary. Our readers should perceive us to have been
  decisive.

--- Remember the old joke about the concert violinist who got lost on his way to a performance?
He stopped an old man on the corner and asked him how to get to Carnegie Hall.
The old man looked at the violinist and the violin tucked under his arm, and said: “Practice,
son. Practice!”

- TODO: you should be using an editing environment that highlights or colorizes members to make them distinct

- "clarity is king" - professional programmer

# Names

- Use Intention-Revealing Names - int d (need to be: elapsedTimeInDays;)
- Avoid Disinformation - accountList (why List?, just accounts is enough)
- Make Meaningful Distinctions (instead of moneyAmount -> money) - Distinguish names in such a way that the reader knows what the differences offer.
- Use searchable names

- Class Names - noun
- Method names - verb

  - accessors - named with 'get'
  - mutators - named with 'set'
  - predicates - named with 'is'

- Pick One Word per Concept - fetch retrieve or get (ONLY ONE)
- Don’t Pun - Avoid using the same word for two purposes
- Use Solution Domain Names - The name AccountVisitor means a great deal to a programmer who is familiar with the VISITOR pattern
- Use Problem Domain Names - business or user needs
  In short, problem domain is about the business or user needs, while solution domain is about how those needs are technically addressed

Reddit thought: When you write code for others to read you need to give them the choice to stay on the surface or go deeper if it’s important for them to understand what lies in the layers below. When you read an article in a news portal for example, you have the headline. That gives you an idea of what that article is about. If you want to know more about it you have the first paragraph trying to summarize everything. If you still need more detail you read the next, and the next and so on. Code is the same thing. When I read code I want to know what an if block does, but I might not want to know how it’s implemented. If you put all the code right there, in nested ifs, or in a chain of else ifs, you’re forcing the reader to read everything to understand what you’re doing. Uncle Bob gives some good examples here: https://youtube.com/playlist?list=PLmmYSbUCWJ4x1GO839azG_BBw8rkh-zOj

# Functions

- Functions must to be small
- Do one thing "FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY."
- Should do only those steps that are one level below the stated name of the function
  - Example: (AddPerson function, the checks/validation can be extracted in methods)
- Keep in mind "TO" - One thing, dedicate function to perticular thing - "To include the setups and teardowns, we include setups, then we include the test page content, and then we include the teardowns. To include the setups, we include the suite setup if this is a suite, then we include the regular setup. To include the suite setup, we search the parent hierarchy for the “SuiteSetUp” page and add an include statement with the path of that page. To search the parent..."

- functions should have 3 parameters at max, mondaic (one parameter), dyadic (two params in relation), triads (three params in relation)
- verbs and keywords - writeField(name), assertExpectedEqualsActual(expected, actual)

- Duplication may be the root of all evil in software
- Functions are the verbs, Classes are the nouns (the domain can be determined from the requirement document)
- Master programmers think of systems as stories to be told rather than programs to be written

# Comments - “Don’t comment bad code — rewrite it.”

- Code changes and evolves - we can not move commend always as we forgive (focus on writing expressive code)
- To be expressive: In many cases it’s simply a matter of creating a function that says the same thing as the comment you want to write.
- You need to care about comments - try without them first - later write the best comment (accurate)
- Still, you don’t want your code to be littered with TODOs. So scan through them regularly and eliminate the ones you can.
- Do not write Redundant Comments
- Misleading Comments - do not explain something that you can not
- Mandated Comments - not every function should have explained comments

- Refactoring
  - it takes time to understand code (do not force yourself too much)
  - know when to dive deeper - to ask yourself always, to save time! (visualization to have, you can not understand everything)
  - ENJOY IT - the collest thing of engineering

# Formatting

- if on team - all members need to comply: automated tool that can apply those formatting rules for you.
- No matter the size of the system - you need to impose how long a source file should be

150-200 lines vertical

- Vertical Openness Between Concepts - blank lines
- Vertical Density - related components to be close as possible, Concepts that are closely related should be kept vertically close to each other
- Vertical Distance - how important each is to the understandability of the other method/Class
- Instance variables - at the top
- Dependent Functions - If one function calls another, they should be vertically close, and the caller should be above the callee, if at all possible

80-100 characters per line

- Horizontal Openness and Density - white space between important things, example: (a + b) / 2

# Objects and Data Structures

Think about visibility - Why, then, do so many programmers automatically add getters and setters to their objects, exposing their private variables as if they were public?

- We do not want to expose the details of our data. Rather we want to express our data in abstract terms
- Difference between objects and data Structures
  - object hide their data behind abstraction, expose functions that operate on that data
  - data stuctures expose their data and have no meaningful functions
    (Hiding data and exposing methods is not enough to create an object (it is still a struct), you have to consider if the methods actually expose behavior or just the data!)

### The Law of Demeter

More precisely, the Law of Demeter says that a method f of a class C should only call
the methods of these:
• C
• An object created by f
• An object passed as an argument to f
• An object held in an instance variable of C

```c#
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
```

```c#
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```

- if ctxt, opts, scratchDir are objects - then we have to much knowledge and change the behavior -> violation of the demeter law
- if it is a data structure and have no behavior -> it's fine

- What if we want to know the internals of the object?
- we can do this with saying what the object need to DO instead of saying GET something

bad: ctx.getScratchDirectoryOption().getAbsolutePath()
good: BufferedOutputStream bos = ctxt.createScratchFileStream(classFileName);

- DTOs are data structures
- Entity/Active Record is data structure

# Error Handling

- Error handling is important, but if it obscures logic, it’s wrong.
- who is reponsible to throw the error - not the algorithm itself but the operation that can throw exception

- use unchecked exceptions - c# uses them

  - checked exception violates Open/Closed Principle - internal "throw" results every method to have changes
  - checked exceptions violates the idea of handling errors (at a distance) -> breaks encapsulations in this way

- Provide Context with Exceptions - Create informative error messages and pass them along with your exceptions, Mention the operation that failed and the type of failure

- Define Exception Classes in Terms of a Caller’s Needs - can classify by their source, our most important concern should be how they are CAUGHT

  - we can make one exception that union all and a wrapper class for out third party provider to wrap the error handling
  - can change provider, better testing, we can encapsulate some unnecessary logic

- Don’t Return Null - think always when it is good and when it is bad to return null (instead you can return empty collection)
- Don’t Pass Null - in my opinion - never

# Boundaries

- Third Party Libraries - We are not suggesting that every use of Map be encapsulated in this form. Rather, we
  are advising you not to pass Maps (or any other interface at a boundary) around your
  system. If you use a boundary interface like Map, keep it inside the class, or close family
  of classes, where it is used. Avoid returning it from, or accepting it as an argument to,
  public APIs.

- Exploring and Learning Boundaries - prototyping when you want to integrate library/API, just a simple console application to see if this package works
  - encapsulate some package

- Learning Tests Are Better Than Free - write learning tests to test the behavior of new release and be adaptible to migrate to new versions

- Using Code That Does Not Yet Exist - defining interface how we want and later adapter to connect the API with our system

# Unit Tests

- The Three Laws of TDD

  - First Law You may not write production code until you have written a failing unit test.
  - Second Law You may not write more of a unit test than is sufficient to fail, and not compiling
    is failing.
  - Third Law You may not write more production code than is sufficient to pass the currently
    failing test.

- Test code is just as important as production code. It
  is not a second-class citizen. It requires thought, design, and care. It must be kept as clean
  as production code.

- A Dual Standard - There are things that you might never do in a
  production environment that are perfectly fine in a test environment. Usually they involve
  issues of memory or CPU efficiency. But they never involve issues of cleanliness.

- One Assert per Test - I think the single assert rule is a good guideline. I usually try to create a domainspecific
  testing language that supports it, as in Listing 9-5. But I am not afraid to put
  more than one assert in a test. I think the best thing we can say is that the number of
  asserts in a test ought to be minimized.

- Single Concept per Test - So probably the best
  rule is that you should minimize the number of asserts per concept and test just one concept
  per test function. (You can miss a case)

- FIRST
  - Fast - opportunity to run tests frequently
  - Independent - should not depend on each other
  - Repeatable - run on each environment
  - Self-Validating - the test should stay if it fails
  - Timely - thing always about testing - to not be hard to test components later (just before production to be written)

- Invent testing APIs that act as domain-specific language that helps you write the tests.

# Classes

- Classes Should Be Small! - our measurement - single responsibility principle - one responsibility (or reasons to change)

  - The name of a class should describe what responsibilities it fulfills. In fact, naming
    is probably the first way of helping determine class size.
    - try to clarify the classes that contain "Processor", "Manager" or "Super" - often hint at unfortunate aggregation of responsibilities
    - We should also be able to write a brief description of the class in about 20 words, without using the words “if,” “and,” “or,” or “but.”

  - We want our systems to be composed of many small classes, not a few large ones. 
    Each small class encapsulates a single responsibility, has a single reason to change,
    and collaborates with a few others to achieve the desired system behaviors.

- Cohesion - high cohesion means the variables and methods are on the right place
  - You should try to separate the variables and methods into two or
    more classes such that the new classes are more cohesive.
  - When classes lose cohesion, split them!
    (one big function with many variables -> many functions with params passed -> instance variables but used with a few functions -> new class -> better cohesion)

- Organizing for Change - a great question to ask - Will this component need changes? (new functions, fileds)
  - if the answer is yes -> try to structure the system to comply with SRP and OCP
- Isolating from Change - adhere to Dependency Inversion Principle

# Systems - stay at the system level

- Separate Constructing a System from Using It
  - startup construction (Program.cs) need to be separated from the logic
  - Lazy-initialization (initialize concrete intance within the method) is not the best solution, we should have a global strategy for resolving dependencies
  - Example of strategy is Dependency Injection (separated container, responsible for initializing the dependencies)
  - As it is software - use the iterative and incremental agility to improve the engineering (it's a lot harder with physical systems)

  - cross-cutting concerns - affect multiple parts of the application and cannot be cleanly encapsulated in a single module or layer (example of cross0cutting concern: EF core spreaded across multiple layers or modules)
    - aspect-oriented programming help to reduce these cross-cutting concerns (can be implemented with Decorator Pattern)
  - noninvasive - means minimal changes, loose coupling, pluggability
  - DSL (Domain Specific Language) - propagates the correct usage of a system
  - Whether you are designing systems or individual modules, never forget to use the simplest thing that can possibly work.

# Emergence

- Four rules for well-designed software
  - Run all tests
  - Contains no duplication
  - Expresses the inent of the programmer
  - Minimizes the number of classes and methods
- No Duplication - extract common logic
  - Template Pattern - common technique for removing higher-level duplication
- Code should clearly express it's intent
- Keep the count of functions and clases small, be pragmatic

# Concurrency

- Concurrency is a decoupling strategy. It helps us decouple what gets done from when it gets done

- Concurrency Defense Principles - prevent two threads to edit shared resource
  - Recommendation: Keep your concurrency-related code separate from other code.
  - Recommendation: Take data encapsulation to heart; severely limit the access of any data that may be shared.
  - Recommendation: Attempt to partition data into independent subsets than can be operated on by independent threads, possibly in different processors.

- Know Your library - Review the classes available to you
  - use the provided thread-safe collections: ConcurrentDictionary
  - use the Executor Framework for Executing Unrelated Tasks: TPL
  - use nonblocking solutions
  - several classes are not thread safe: List

- Know Your Execution Modoles
  - Producer-Consumer
  - Readers-Writers
  - Dining Philosophers - TODO: Recommendation: Learn these algorithems and understand their solutions

- Writing Correct Shit-Down Code is Hard - Think about shut-down early and get it working early. It’s going to
take longer than you expect. Review existing algorithms because this is probably harder than you think.
- Do not ignore system failures as one-offs.

- Force failures with instrucments - Use jiggling strategies to ferret out errors.
  - hand-coded
  - automated

# Successive Refinement

- To write clean code, you must first write dirty code and then clean it
- You need repetitive refinements to achieve good design
- A great example of refactored code is the - Args: The Rough Draft (TODO: play more with it)
- You need to know when it's time to stop adding features, and try to refactor the codebase 
- When refactor - try to refactor without breaking the system, at each change the system should work

# JUnit Internals

- Encapsulate logic to be easier for readers
- Should not have variables in a function with the same name of member variables
- Negatives are slightly harder to understand (canNotCompact -> canBeCompacted)
- Having member variables exposes threat to "hidden temporal coupling"
- try to apply Boy Scout Rule!

# Refactoring SerialDate

- First, Make it Work
  - write more unit tests
  - TODO: Check about coverage tool
- Then, Make it Right
  - abstract class - know the level of abstraction in order to name it (DayDate instead of SerialDate)

# Smells and Heuristics

- Practice refactoring
  - Comments
    - Inappropriate Information - every thing neeed to have place (issue tracking system should be separated instead of be as comments in the source code)
    - Obsolete comment
    - Redundant comment
    - Poorly Written comment
    - Commented-Out code - delete it, the source control system still remembers it
  - Environment
    - Build Requires More Than One Step - it should not
    - Tests Requires more than one step - it should not
  - Functions
    - Too many arguments - avoid mant arguments
    - Output arguments - not intuitive, avoid if you can
    - Flag arguments
    - Dead functions - remove it
  - General
    - Multiple Languages in one source file - keep the number low as you can
    - Obvious Bheavior is unimplemented - keep functions described as possible
    - Incorrect Behavior at the boundaries - Look for every boundary condition and write a test for it.
    - Overriden Safeties - It is risky to override safeties
    - Duplication  - missed opportunity for abstraction
      - use design pattern where sutable
      - db normal forms
      - Object-oriented programming
    - Code at wrong level of abstraction
      - abstract classes and derivatives - (constants, variables, utilities - pertain to the implementation)
      - true for source files, components, modules
      - do not expose functions in the abstract class that will not be used by the derivatives
    - Base classes depending on their derivatives
      - Base classes depending on their derivatives - base classes should know nothing about their derivatives
    - Too much information
      - learn what you need to expose at the interfaces of classes and modules (coupling is low!)
    - Dead code - delete it
    - Vertical Separation - how easy is to find your private function?
    - Inconsistency - example: variable response/request - use the same over the code
    - Clutter - remove the clutter
    - Artificial Coupling
      - enums should not depend on specific classes (what if other class need to use this enum, will need to know about the whole class)
      - static utils functions - separated from classes
    - Feature Envy - avoid it, it exposes the internals of one class to another
    - Selector Arguments - beeter to have many functions than to pass some code into a function to select the behavior
    - Obscured Intent
    - Misplaced Responsibility - it's all about where the function should be and is it's name correct
    - Inappropriate static - prefer nonstatic methods to static methods. When in doubt, make the function nonstatic
      If you really want a function to be static, make sure that there is no chance that you’ll want it to behave polymorphically
    - Use Explanatory Variables - break calculations into intermidiate values
    - Functions Names Should Say What They Do - you need to understand the function from the name/signature
    - Understand the Algorithm - understand how it works
    - Make Logical Dependencies Physical - chain the intended dependency (page size should be in the appropriate class, not in both)
    - Prefer Polymorphism to if/else or switch/case
    - Follow Standard Conventions
    - Replace Magic Numbers with Named Constants
    - Be Precise 
    - Structure over Convention
    - Encapsulate Conditions
    - Avoid negative conditions
    - Functions should do one thing
    - Hidden Temporal Couplings - use the di principle here
    - Do not be arbitrary
    - Encapsulate boundary conditions
    - Functions should descend only one level of abstraction - This points out that when you break a function along lines of abstraction, 
      you often uncover new lines of abstraction that were obscured by the previous structure.
    - Keep Configurable Data at High Levels
    - Avoid Transitive Navigation
  - Java
    - Avoid Long Import Lists by using wildcards
    - Do not Inherit Constants
    - Constants versus Enums
  - Names
    - Choose Descriptive Names
    - Choose Names at the Appropriate Level of Abstraction
    - Unambiguos names
    - Use Long Names for Long Scopes
    - Avoid Encodings
    - Names should describe side-effects
  - Tests
    - Insufficient Tests
    - Use Coverage Tool - quich and easy to find "if" or "catch" statements whose bodies have not bee n checked
    - Do not Skip Trivial Tests
    - An Ignored Test is a Question about an Ambiguity
    - Test Boundary Conditions
    - Exhaustively Test Near Bugs
    - Patterns of Failure Are Revealing
    - Test Coverage Patterns Cna be Revealing
    - Tests Should be Fast

# Bonus

Reddit thought: When you write code for others to read you need to give them the choice to stay on the surface or go deeper if
it’s important for them to understand what lies in the layers below. When you read an article in a news portal for example,
you have the headline. That gives you an idea of what that article is about. If you want to know more about it you have the
first paragraph trying to summarize everything. If you still need more detail you read the next, and the next and so on. 
Code is the same thing. When I read code I want to know what an if block does, but I might not want to know how it’s implemented. 
If you put all the code right there, in nested ifs, or in a chain of else ifs, you’re forcing the reader to read everything to understand 
what you’re doing. Uncle Bob gives some good examples here: https://youtube.com/playlist?list=PLmmYSbUCWJ4x1GO839azG_BBw8rkh-zOj

## Lesson 1
  - we make the mess because of the desire to be faster
  - when the code works - there is another half of the work - to clean the code
  - the only way to go fast is to go well!
  - every line of a function should be at the same level of abstraction - it is rude if not
    - that level should be one below the name of the function
  - function should be really small - to do one thing
  - every large function is a class with with fucntions and variables to manipulate
  - max 3 arguments for a function
  - the code do not need to have double take moments (watch something more than once)
  - we are Engineers - we are responsible
  - why to not use Switch statements: 
    - too many places to edit if we introduce something new!
    - recompling, redeploying, TODO: compile, deploy, good practices
  - a function that has void - need to have side effect (change the state of a system)
  - a function that has return value - need to no have side effect
  - test every individual line you wrote

## Lesson 2
  - Without excuses - you are responsible for the code
  - Design Patterns matter - TODO: Read the book: Design Patterns
    - the fastest way to understand the whole design by simple stating the name of the design pattern in the class's name
  - Do not talk about code (through comments) that is somewhere else
  - If you write comments - you need to have a good reason
  - A variable name length should be proportional to the size of the scope that contains it
    - in a single line "for loop" - one letter will be perfect (example: i)
    - function varibales - one word
    - instance variables - two words
    - global variables - more

    - functions are the opposite - if the scope is smaller - the name is bigger
      - private functions - longer names
      - private called by private - longer and precise

## Multithreading - all parallel programs are concurrent, but not all concurrent programs are parallel - parallel is a subset of Concurrency
    - Concurrency - two threads on same core - the goal is to have not blocking application
      - it is undeterministic, which will finished first, the final output is deterministic
      - hard for debugging
    - Parallelism - two threads on different cores - the goal is performance
      - easier for debugging

  - Asynchronous code does not create threads - it uses concept of state machines internally
  - Without synchronization context Async can spawn threads to execute the remaining part of the code

- https://medium.com/devtechblogs/overview-of-c-async-programming-with-thread-pools-and-task-parallel-library-7b18c9fc192d
- https://devblogs.microsoft.com/premier-developer/dissecting-the-async-methods-in-c/
- https://learn.microsoft.com/en-us/archive/msdn-magazine/2013/march/async-await-best-practices-in-asynchronous-programming
