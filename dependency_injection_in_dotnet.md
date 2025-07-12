# Dependency Injedction in .NET

Author: Mark Seemann

N-tier architecture style
The tools are only useful if your are building systems that incorporate the patterns that the tools are addressing
The purpose of DI => create maintainable software within the object-oriented paradigm

Good learning approach:
- clear your mind and learn what the thing truly is
- see how professionals doing is, just watch
- do it yourself

# Part 1 - Putting Dependency Injection on the map

## A Dependency Injection tasting menu

Definition: DI is a set of software design principles and patterns that enable us to develop loosely coupled code

You should stating a need with DI - "I need something to drink with lunch" (instead of making/seaching for it)
Collaborating classes should rely on the infrastructure to provide the necessary services

Knoledge: Program to an interface, not an implementation

- Late binding - replace parts of an application without recompiling the code (we depend on abstraction rather than on implementation), late binding is one of the many aspects of DI
- Unit testing - one of the aspects of DI
- An abstract factory on steroids - DI is not a service that can be used to get dependencies - this is Service Locator
    - it's a way to structure code so that we never have to ask for dependencies (we force consumers to supply them)
- DI Containers - optional library that makes it easier to compose components when we wire up an application

1. Writing maintainable code
    - Liskov substitution principle - the ability to replace one end without changing the other
        - it enables us to address requirements for the future, even we can not foresee them
    - Null Object Pattern - we are loosely coupled, we can replace real implementation with something that does nothing (does not explode)
    - Decorator Design Pattern - Intercepting one implementation with another implementation of the same interface (UPS and Computer plug to the wall outlet)
    - Compose Design Pattern - aggregate several implementations into one (power strip makes it possible to have multiple implmentations into a single wall outlet)
    - Adapter Design Pattern - match two related, yet separate, interfaces to each other (third-party API that you expose as an instance of an interface your application consumes)
    The question is, where do the instances come from? In a sense, this is what this entire book is about.
2. Hello DI
    - Constructor Injection - The class requests an instance of interface through its constructor
    - Benefits from loose coupling
        - Late binding - swapping of services - valuable in standard software
        - Extensibility - always valuable
        - Parralel Development - developed in parralel - valuable in large projects
        - Maintainability - easier to maintain - always valuable
        - Testability - easier for unit testing
        - Open/Closed Principle
    - Composition Root - application's entry point
    - The only major obstacle is to figure out how to get hold of instances of those interfaces - DI is the answer

Definition: An application is considered Testable when it can be unit tested

3. What to inject and what not to inject - VOLATILE DEPENDENCIES are the focal point of DI. It’s for VOLATILE DEPENDENCIES, rather than STABLE DEPENDENCIES, that we introduce SEAMS into our application
    - Seams 
        - Everywhere we decide to program against an interface instead of a concrete type, we introduce a SEAM into the application
        - a place where an application is assembled from its constituent parts (SEAM between Salutation ConsoleMessageWriter)
    - Stable Dependencies
        - Framework Library Models - no threat to modularity
        - Important criteria for stable dependencies
            - the class already exists
            - you expect that new versions will won't contain braking changes
            - the types in question contain deterministic algorithms
            - you never expect to have to replace the class with another
        - DI Containers
        - Specialized third-party libraries
    - Volatile Dependencies - dependency that not provide sufficient foundation for the application
        - The symptoms of this type of DEPENDENCY are lack of late binding and extensibility, as well as disabled TESTABILITY.
        - The obvious symptom of such dependencies is the inability to do parallel development (you need to depend on abstraction in this case!)
        - The most common symptom is disabled TESTABILITY

4. DI scope

- a class should not concern how its dependency is created (we don’t lose that control—we only move it to another place)
- with DI we gain the ability to intercept each Dependency before it's passed to the consumer
- With DI, we can compose applications while intercepting dependencies and controlling their lifetimes

- Object Composition - DI is closely tied to it
- Object Lifetime
- Interception - With INTERCEPTION, we can apply CROSS-CUTTING CONCERNS such as logging, auditing, access control, validation,
and so forth in a well-structured manner that lets us maintain Separation of Concerns.
- DI as encompassing all three in a consistent way (Object composition, interception, lifetime mangment)

5. Summary - DI must be pervasive. You can’t easily retrofit loose coupling onto an existing code base

## A comprehensive example
- loose coupling is first and foremost an efficient way to deal with complexity (Complexity is part of the game)
- the most famous architecture for decoupling - 3-layer architecture (ui -> domain (the heart of the application) -> data)

1. Doing it wrong
- building a tightly coupled application
    - you may not realize it at first, but create a Domain Logic Layer (do not include business logic in the controller)
    - evaluate the composability - is tightly coupled, swap modules to see it
        - New UI
        - New Data access layer
    - do not expose data entity for return type from domain logic
    - do not couple data acess with domain logic
    - Product class belongs for the Domain Model
    - Do not have business logic in the UI
    - The caller should consider about configuring the dependency (config files for ef core)
    - The view should be simple as possible
2. Does it right
- DI is a subset of IoC (Inversion of Control)
    - IoC - design pattern where the control flow of a program is inverted (instead of the application controlling the flow (ASP.NET CORE), external frameworks or containers manage the creation and lifecycle of objects)
        - a great example - bob gets car to go to work -> the company is reponsible for getting bob from home (implemented inversion of control)
        - the framework calls me instead of me calling it ("Don't call us, we will call you")
- Contol Freak anti-pattern - the application is in total control (it initialized its dependencies)

- Rebuilding the commerce application
    - focus first on the interface - simple as possible (we can experience testing early as possible here)
    - encompact everthing in its place (create POCOs)
    - use method Injection (know each class responsibility)
- Analyzing the loosely coupled implementation

3. Expanding the sample application
- Architecture - from three-layer -> added Presentation Model (used to split the Views/Composition root with the controllers/ViewModels)

## DI Containers

- DI - is a technique
- DI Containers - the technology that supports the technique

1. Introducing DI Containers
- Definition: A DI CONTAINER is a library that provides DI functionality

- application must first and foremost be designed with the DI patterns and techniques in mind
- In fact, the Resolve method fits the signature of a SERVICE LOCATOR,2 and you’ll need to exercise care not to use your DI CONTAINER as a SERVICE LOCATOR. (do not use Resolve in Domain Layer, rely on Dependency Injection, do not couple the logic)

- Definition: AUTO-WIRING is the ability to automatically compose an object graph from maps between ABSTRACTIONS and concrete types

2. Configuring DI Containers - defien mappings between abstractions and concrete types
- DI configuration options:
    - XML (config settings - .config file) - explicit, supports late binding, no compile-time checks
        - use it only when you need late binding
        - disadvantages - verbosity and brittleness
    - Code as configuration (addscopped()) - explicit
        - we lose the benefit of late binding
        - more compact, compiler support
    - Auto-registration (scrutor)- implicit
        - we can introduce our own conventions (automation for out components)

3. DI Container patterns
- Composition Root - composed together
    - to compose objects as close as possible to the application's entry point
- Service Locator - anti-pattern (example: resolve service in the ctor)
- Register Resolve Release
    - static structure
        - A common source of confusion is that the Three Calls Pattern makes an adamant statement about how often each method must appear in your code base, but it says nothing about how many times they must be invoked.
    - dynamic interaction

4. DI Container landscape
- Decision Process
- Selected DI Containers

# Part 2 - DI catalog

## DI Patterns

1. Constructor Injection - default choice for DI
    - use when you strongly rely on the same dependency
    - appropriate for applications based on frameworks
- Ambient Context - allows automatic access to context-based data (e.g., user information, request data, etc.)
2. Property Injection - also known as SETTER INJECTION
    - PROPERTY INJECTION is best used when the DEPENDENCY is optional (overrding Local Default)
3. Method Injection
    - different for each operation
    - advantage: allows the caller to provide operation-specific context
    - disadvantage: limited applicability
    - appropriate for building a framework
4. Ambient Context - make dependency available to every module without pulling every API with cross-cutting concerns (to not pollute APIs)
    - condtions for implementing it
        - queryable context
        - proper Local Default exists
        - It must be guaranteed available (check for null value)
    - advantages: does not pollute, always available
    - disadvantages: implicit, hard to implement correctly, may not work well in certain runtimes
- Caching is an excelent example of Interception

## DI anti-patterns

- An anti-pattern is a description of a commonly occurring solution to a problem that generates decidedly negative consequences
- Control Freak - the most dominating anti-pattern

1. Control Freak - dependencies are controlled directly, as opposed to Inversion of Control (every time we use "new" keyword)
    - The number of times the new keyword is used in code is a very rough indication of how tightly coupled that code is.
    - Factory
        - Concrete Factory
        - Abstract Factory
        - Static Factory
    - Dependency collapse - the end is monolithic application - bad

2. Bastard Injection - foreign default are used as default values for dependencies
    - Foreign Defaults - opposite of Local Default, default dependency but defined in different module than its consumer
        - in this way we coupled with the other module (bad for changing modules/parallel development)

3. Constrained Construction - constructors are assumed to have a particular signature
    - know your implicit constraints - passing connection string to abstract Repository constrains the implementors to rely on this connection string
    - Modeling DEPENDENCY construction exclusively on explicit constraints (interface or base class) is a much better and more flexible option
    - the idea is to achieve late binding while preserving composability within objects (connection string is still passed as parameter throuhg the ctor)
    - apply when we employ late binding (as in early binding there constrains are resolved during coding/refactoring)

4. Service Locator - an implicit service can serve Dependencies to consumers but isn't guaranteed to do so
    - service locator is a static factory, configured with concrete dependencies
    - ads unneccesary redundancy (can be achieved with Constructor Injection)
    - not intuitive design (we can forget to register it, to pass the dependency)

## DI refactorings

1. Mapping runtime values to Abstractions
    - when abstraction depend on runtime values - use Abstract Factory
        - Abstract Factory - get implementation for something abstract at will (translate a runtime value to concrete dependency)
        - An Abstract Factory is the universal solution when we need to create DEPENDENCIES from runtime values
        - Leaky Abstraction - abstraction factory class without the benefit of choosing the strategy (without user preference/class that determines the created instance)
            - 
2. Working with short-lived dependencies
    - You can model such interactions with an Abstract Factory that produces disposable
instances.
    - You should strive to hide this pattern behind a stateless ABSTRACTION

- Hiding connection managment behind an abstraction
    - encapsulate the open/close action within the abstraction (the consumer does not need to know about open/close stuff)
- Opening and closing dependencies
warning: Stopping one leak creates another. We exchange memory leaks for LEAKY ABSTRACTIONS
warning: Disposable DEPENDENCIES are design smells. Use them only when there is no other option
- It helps resolve runtime DEPENDENCIES and short-lived DEPENDENCIES. We can also include it in an effort to resolve cyclic DEPENDENCIES, but it doesn’t play a central role in that context.

3. Resolving cyclic Dependencies
- A DEPENDENCY cycle is a design smell. If one appears, you should seriously reconsider your design
- Attempt to address cycles by using events. If that fails, try an Observer. Only if you’re still unsuccessful should you consider breaking the cycle by using PROPERTY INJECTION
- Use Property Injection (e.g., DataContext in WPF) to inject dependencies at a later stage
- Use an Abstract Factory to defer the creation of complex dependencies like MainWindowViewModel

4. Dealing with Constructor Over-injection
- if we have 6 params in a constructor - in most cases we violate SINGLE RESPONSIBILITY PRINCIPLE (CONSTRUCTOR INJECTION makes it easy to spot SINGLE RESPONSIBILITY PRINCIPLE violations)
- we can introduce Facade Services - discovering the natural clusters (we can introduce Facade Services that orchestrate parts of the relationship)

5. Monitoring coupling
- how coupled components are - can you remove the concrete dependency

# Part 3 - DIY DI

## Object Composition

1. Composing console application
Tip: The COMPOSITION ROOT should do only two things: set up the container and
resolve the type that implements the desired functionality. As soon as it has done
that, it should get out of the way and leave the rest to the resolved instance.

2. Composing ASP.NET MVC applications
 - extend the defaut DefaultControllerFactory

3. Composing WCF applications
4. Composing WPF applications
5. Composing ASP.NET applications
6. Composing PowerShell cmdlets
