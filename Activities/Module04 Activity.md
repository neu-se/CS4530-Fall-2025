---
layout: page
title: Code-Level Design
nav_exclude: true
---
# Readable Code Activity

### Getting started
Start by downloading the [(Starter Code)]({{ site.baseurl }}{% link Activities/module04-traffic-light-activity.zip %}).
Run `npm install` to download the dependencies for this project, and then open it in your IDE of choice. 
Run `npm run test` to run the tests of the existing code (or run the script in VSC).  You will see that the tests pass.

### The Problem

Your team is writing a simulator for a traffic light in a large city.  Whitley, an intern in your group, has written the code in TrafficLight.ts, and the tests in TrafficLight.test.ts

Your team leader, Adrian, has asked you to critique Whitley's code based on the Five Code-Level Design Principles.  Adrian says that he has already received some feedback from the client, who complained that the code expects all lights to display red to be on for 20 seconds, yellow for 5 seconds, and green for 15 seconds, but there are traffic lights in the city that do not conform to that pattern.  They may have different display times, or they may have different symbols as well (e.g. left-turn arrows, etc.)

### The Task

Write a new file, called `betterTrafficLight.ts`, which uses the Principles of this module to address some of the problems raised by the customer.  Put comments in your code that document your improvements. Test your code by changing `TrafficLight.test.ts` to import from `betterTrafficLight.ts`.  Your code should pass the tests in `TrafficLight.test.ts` without change.  

The package for this activity contains a npm script to run stryker, so you can judge the adequacy of your tests.  We encourage you to do so.

### Submit your work

Submit the file `betterTrafficLight.ts`.  You are *not* required submit your tests.

Be sure to review Canvas assignment for submission and any other related details (if assigned).


