# test-driven-development
##What are unit tests?
According to Wikipedia : 


    In computer programming, unit testing is a software testing method by which individual units of source
    code—sets of one or more computer program modules together with associated control data,
    usage procedures, and operating procedures—are tested to determine whether they are fit for use.

In other words, unit tests are not about testing individual methods or functions (which is a common misconception) but about testing a unit of behavior. This means that the real unit, is the test itself, as it needs to be able to evaluate the behavior under test independently from other behaviors, and therefore, independently from other tests. The real unit is the test itself, not the object under test, since we’re not testing individual objects, but complex behaviors whose code might go through a variety of objects, classes, functions, etc.

A failing test shouldn’t affect the result of other tests.

##TDD is not testing
Lots of people associate TDD with testing, this is also a common misconception. TDD is not a testing method. It’s a development method. It's about finding the algorithm. It's about using tests to "ask questions" that your algorithm will answer as you develop it.
TDD uses tests to develop, but it isn’t a testing strategy. It isn’t about testing.

There are 2 main schools of thoughts in TDD :

* The London school (or also mockist), that advocates for outside-in t
* The Chicago School (or also classicist)

The description of those 2 schools of thoughts is beyond the scope of this presentation, however, both have one thing in common

##Hexagonal architecture, and how TDD helps your design
The hexagonal architecture, or ports and adapters architecture, is an architectural pattern used in software design. It aims at creating loosely coupled application components that can be easily connected to their software environment by means of ports and adapters. This makes components exchangeable at any level and facilitates test automation.

TDD, by making you start with writing your tests before writing your code, forces you to test from your public API, this indirectly helps you towards hexagonal architecture naturally as everything needs to be testable from the start. It won’t do everything for you, but if you have basic notions of architecture and design patterns, it will naturally guide you towards a decoupled design, and will help you have a public API loosely coupled to your external dependencies.
You can then have your public API receive adapters that are nothing more that just wrappers around your dependencies and those same adapters can easily be faked (more often than not, those are stubs) in order to make your tests fast and efficient.

 

INSERT GRAPH of hexagonal architecture with tests around the hexagon and adapters

Give an example of design with hexagonal architecture and tests for an animation library.

Start from a list of features : 

* save a pose
* load a pose
* save an animation
* load an animation
* load a series of poses to create an animation
* load a series of animations to create an animation

Fakes : difference between mocks and stubs
Don't mock what you don't own => create adapters around your dependencies : that's what hexagonal architecture is for
