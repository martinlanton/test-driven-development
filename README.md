# test-driven-development

This page is a presentation about some parts of the concept of unit testing in Python. Most of it is specifically about Test-Driven Development and introduces its related disciplines : Behavior Driven Development (BDD) and Acceptance Test-Driven Development (ATDD).

Those 2 related disciplines however are beyond the scope of this presentation, so we will just introduce them and their relation to TDD.

## What are unit tests?
According to Wikipedia : 


    In computer programming, unit testing is a software testing method by which individual units of source
    code—sets of one or more computer program modules together with associated control data,
    usage procedures, and operating procedures—are tested to determine whether they are fit for use.

In other words, unit tests are not about testing individual methods or functions (which is a common misconception) but about testing a unit of behavior. This means that the real unit, is the test itself, as it needs to be able to evaluate the behavior under test independently from other behaviors, and therefore, independently from other tests. The real unit is the test itself, not the object under test, since we’re not testing individual objects, but complex behaviors whose code might go through a variety of objects, classes, functions, etc.

A failing test shouldn’t affect the result of other tests.

## TDD is not testing
Lots of people associate TDD with testing, this is also a common misconception. TDD is not a testing method. It’s a development method. It's about finding the algorithm. It's about using tests to "ask questions" that your algorithm will answer as you develop it.
TDD uses tests to develop, but it isn’t a testing strategy. It isn’t about testing.

There are 2 main schools of thoughts in TDD :

* The London school (or also mockist), that advocates for outside-in t
* The Chicago School (or also classicist)

The description of those 2 schools of thoughts is beyond the scope of this presentation, however, both have one thing in common

## Hexagonal architecture, and how TDD helps your design
The hexagonal architecture, or ports and adapters architecture, is an architectural pattern used in software design. It aims at creating loosely coupled application components that can be easily connected to their software environment by means of ports and adapters. This makes components exchangeable at any level and facilitates test automation.

TDD, by making you start with writing your tests before writing your code, forces you to test from your public API, this indirectly helps you towards hexagonal architecture naturally as everything needs to be testable from the start. It won’t do everything for you, but if you have basic notions of architecture and design patterns, it will naturally guide you towards a decoupled design, and will help you have a public API loosely coupled to your external dependencies.
You can then have your public API receive adapters that are nothing more that just wrappers around your dependencies and those same adapters can easily be faked (more often than not, those are stubs) in order to make your tests fast and efficient.

 

INSERT GRAPH of hexagonal architecture with tests around the hexagon and adapters

Give an example of design with hexagonal architecture and tests for an animation library.

Start from a list of features : 

* save a pose
  * save a selected empty pose (no keyframes) : save nothing
  * save a selected pose
* load a pose
  * load an empy pose (empty file) : load nothing
  * load a corrupted file : load nothing
  * load a single pose : load the pose at specified frame
* save an animation
  * save an empty frame range : save nothing 
  * save the keys over a certain frame range
* load an animation
  * load an empty animation file : load nothing
  * load an animation at the specified start frame
  * load an animation at the specified start frame with an already existing animation : should error when not in force mode
  * load an animation at the specified start frame with an already existing animation : should erase the current animation when in force mode
* load a series of poses to create an animation
  * load a series of empty poses at specified start frame and interval : load nothing
  * load a series of poses, some of which empty, at specified start frame and interval : should leave empty frames in the timeline based on the interval specified and the order of empty poses
  * load a series of poses at specified start frame and interval
  * load a series of poses at specified start frame and interval with an already existing animation : should error when not in force mode
  * load a series of poses at specified start frame and interval with an already existing animation : should erase the current animation when in force mode
  * load a series of poses over specified frame range with specified interval (should stretch/squash interval to fill the frame range)
  * load a series of poses over specified frame range with specified interval with an already existing animation : should error when not in force mode
  * load a series of poses over specified frame range with specified interval with an already existing animation : should erase the current animation and stretch interval to fill the frame range when in force mode
* load a series of animations to create an animation
  * load a series of empty animations at specified start frame and interval : load nothing
  * load a series of animations, some of which empty, at specified start frame and interval : should leave empty frames in the timeline based on the interval specified and the order of empty animations (and/or the length of empty animations, if specified)
  * load a series of animations at specified start frame and interval
  * load a series of animations at specified start frame and interval with an already existing animation : should error when not in force mode
  * load a series of animations at specified start frame and interval with an already existing animation : should erase the current animation when in force mode
  * load a series of animations, some of which empty, over specified frame range and interval : should leave empty frames in the timeline based on the interval specified and the order of empty animations (and/or the length of empty animations, if specified)
  * load a series of animations over specified frame range and interval : should stretch/squash animations to fill frame range
  * load a series of animations over specified frame range and interval with an already existing animation : should error when not in force mode
  * load a series of animations over specified frame range and interval with an already existing animation : should erase the current animation stretch/squash loaded animations to fill frame range when in force mode
* load a series of animations to create an COMBINED animation : same thing as the precedent series of test, but with the addition that the last frame of an animation should be replaced with the first frame of the following animation
  * load a series of empty animations at specified start frame and interval : load nothing
  * load a series of animations, some of which empty, at specified start frame and interval : should leave empty frames in the timeline based on the interval specified and the order of empty animations (and/or the length of empty animations, if specified)
  * load a series of animations at specified start frame and interval
  * load a series of animations at specified start frame and interval with an already existing animation : should error when not in force mode
  * load a series of animations at specified start frame and interval with an already existing animation : should erase the current animation when in force mode
  * load a series of animations, some of which empty, over specified frame range and interval : should leave empty frames in the timeline based on the interval specified and the order of empty animations (and/or the length of empty animations, if specified)
  * load a series of animations over specified frame range and interval : should stretch/squash animations to fill frame range
  * load a series of animations over specified frame range and interval with an already existing animation : should error when not in force mode
  * load a series of animations over specified frame range and interval with an already existing animation : should erase the current animation stretch/squash loaded animations to fill frame range when in force mode

Fakes : difference between mocks and stubs
Don't mock what you don't own => create adapters around your dependencies : that's what hexagonal architecture is for
