---
layout: page
title: User Stories and Conditions of Satisfaction
permalink: /tutorials/week1-user-stories
parent: Tutorials
nav_order: 3
---
This tutorial provides examples for user stories, conditions of satisfaction and how a minimum viable product can be defined.

Contents:

* [User Stories and Conditions of Satisfaction](#user-stories-and-conditions-of-satisfaction)
* [User Stories and Project Planning](#user-stories-and-project-planning)
* [User Stories and Test-Driven Development](#user-stories-and-test-driven-development)
* [Examples](#examples)

# User Stories and Conditions of Satisfaction

A user story is an informal, general explanation of a software feature written from the perspective of the **end user or customer**. A user story is always of the following form:

As a <code>&lt;role&gt;</code> I can <code>&lt;perform action&gt;</code> so that I can <code>&lt;receive benefit&gt;</code>

User stories represent something the user/customer might want. There will be many ways to give the user/customer the benefit that they want.

We need to refine these in order to determine what to build. We call these refinements “conditions of satisfaction” (COS)

A COS should be a specific capability or behavior that the user expects, in the user’s terms.  It should be visible to and verifiable by the user.

The COS is a guide to the implementation team. It should be specific enough so that the implementation team has a clear idea of what they are building.
There still may be many ways to implement a COS. For example, a COS probably would not specify any of the graphic or layout details; these would likely be left to the implementation team.

# User Stories and Project Planning

In planning a project, need to assign priorities to each user story and Condition of Satisfaction. Priorities tell us the order in which COS and their associated engineering tasks should be addressed, and how much effort should be devoted to each of them.
There are many ways to describe priorities. For example, a user story might be described as Essential, Desirable, or Extension:

* **Essential** means the project is useless without it.
* **Desirable** means the project is less usable without it, but is still usable.
* **Extension** describes a User story or COS that is desirable, but may not be achievable within the scope of the project.

## Minimum Viable Product (MVP)

An MVP is a product that consists of all essential user stories. Developers should prioritize those above others.

# User Stories and Test-Driven Development

We model the development process as a cycle of refinements:

1. User Stories
2. Conditions of Satisfaction
3. Testable behaviors
4. Executable Tests
5. Engineering Tasks (Code)

As we proceed down these refinements, we will likely go back and revisit design decisions that we made at earlier stages. This is the topic of Module 02.

# Examples

## User Stories

### User Story #1

As a user of stack overflow, I want to be able to reply to questions with answers so that I can help others with my knowledge. (Essential)

### User Story #2

As a user of stack overflow, I want to be list my replies and how often they are upvoted so that I can see how well people react to my answers.  (Desirable)

## User Story #3

As a user of stack overflow, I want to be able to play the codel (like the wordle but for code) so that I can enjoy my time on the site. (Extension)

## Conditions of Satisfaction

### For User Story #1

* There should be a place on questions to post my reply with an answer (Essential)
* Replies should be visible to anyone who views the question (Essential)
* I should be able to format my reply with syntax highlighting. (Desirable)
* Replies should pop up in real-time without needing to reload the page (Extension)

### For User Story #2

* I should be able to view a list of my replies and how many upvotes they have each received. (Essential)
* I should be able to click on a reply from the list and it links me to the appropriate page. (Desirable)
* Other users should be able to see my replies and total number of upvotes (Desirable)
* I should be able to compare my total number of upvotes with all the other users on the site. (Extension)

### For User Story #3

* I should be able to play the codel and use my knowledge of programming languages and practices to solve puzzles. (Essential)
* Everyday the puzzle should change to something new. (Essential)
* I should be able to share how well I did on the codel without spoiling the answer. (Desirable)
* Puzzles should generate randomly so there is always a new puzzle. (Extension)

[Reference](https://www.simplilearn.com/tutorials/agile-scrum-tutorial/user-stories#how_to_write_user_stories)
