---
layout: page
title: Requirments Engineering -- VSD, User Stories, and Conditions of Satisfaction
permalink: /tutorials/week1-user-stories
parent: Tutorials
nav_order: 3
---
This tutorial provides a description of Value Sensitive Design (VSD) and the process of applying it to define 
user stories. Further, it provides examples for user stories, conditions of satisfaction and how a minimum viable product can be defined. The process description and the examples will help understand the process of collecting requirements
as user stories and how to document them in a systematic way.

Contents:

* [What is VSD?](#what-is-vsd)
* [User Stories and Conditions of Satisfaction](#user-stories-and-conditions-of-satisfaction)
* [User Stories and Project Planning](#user-stories-and-project-planning)
* [User Stories and Test-Driven Development](#user-stories-and-test-driven-development)
* [Examples](#examples)

# What is VSD?

Like any technology, software reflects and affects human values. Ignoring values during the requirements collection and definition phase is irresponsible as it leads to software whose impact on communities that use it may be unintentional at best or actively harmful at worst. 

Value sensitive design (VSD) is a framework to systematically reason about values in software design. This involves the following:

- Combine empirical, value, and technical investigations
- Recognize the stakeholders involved and consider their values.
- Consider diverse perspectives.

The three types of investigation -- empirical, value, and technical into a value often require collaboration with experts in different fields ranging from sociology to philosophy to computer science. While this is difficult to practice without
access to a diverse team, this tutorial, through a few examples, will help you appreciate how the process can be applied to requirements gathering.

Before proceeding it is helpful to note what VSD is not! VSD does not prescribe a system of ethics or specific values, rather it incorporates value reflections in the requirements choosing process. 

## Informed Consent Online Example

Web applications today are pervasive. They have access to huge amounts of personal information to enable important
services to banking, education, entertainment, etc. Often such information is collected surreptiously, without the user's
consent. One way to address this problem is to encrypt personal data and prevent unauthorized access. However, solutions like encryption place the burden on automated technical mechanisms, with the software engineer as adjudicator. Another way is through informed consent, in which direct and indirect stakeholders, based on how the application works, choose whether to provide their personal data or not. 

To understand informed consent, we need to investigate how the concept works in the real-world (empircal) and reflect on how the concept may manifest in different ways (value investigation). The idea hinges on two concepts -- informed and consent. Informed encompasses *disclosure* and *comprehension*. Disclosure refers to providing accurate information about
the pros and cons of taking an action. If the action involves collecting personal information then the following should be made explicit: (1) what is being collected, (2) who will have access to it, (3) how long will it be stored, (4) what will it be used for, and (5) whether the data will be anonymized. Comprehension is complex in a digital or virtual environment due to the lack of face-to-face interactions. Hence as designers, we will need to analyze the interventions that need to be
created to ensure that the users understand the disclosures (e.g., a quiz). 

The second construct of *consent* encompasses *voluntariness*, *competence*, and *agreement*. *Voluntariness* simply means to ensure that the action was not coerced or manipulated. For e.g., the decision to accept or reject disclosure will affect essential usage. *Competence* refers to the mental and physical capabilities needed to give consent. For e.g., web applications meant for children will need to be mindful of this component. Finally, *agreement* refers to a clear opportunity to accept or decline participation. For e.g., in this context, the ability to accept or reject must be visible and
accessbile and not obscured in layers.  

Now that we have reasoned about the idea of informed consent in our context, we need to think of the stakeholders that will be affected by this requirement. Considering different stakeholder viewpoints is a part of the value investigation process. Stakeholders can be direct, that is those who directly interact with the system, and indirect, that is those who don't but are affected nevertheless. For the system we are developing, site users are direct stakeholders as they will interact with the system that will eventually implement informed consent. On the other hand, there are indirect stakeholders that might be affected such as site owners, advertising partners, and regulators. This list is by no means comprehensive. The more diverse stakeholders you can think of the more wholistic your requirements will be. Of course they
also have to be realistic.   

Often stakeholders can have different goals, interests, and values. Sometimes they can align and other other times they might conflict with each other. For e.g., site users might want to browse the site anonymously whereas site owners might want to monetize site usage by making personal data available to advertisers. Value investigation also includes resolving such tensions in the requirements collection phase. Suppose for our system, we have identified that the following values are important for our stakeholders -- privacy for site users, accountability for site owners, transparency for advertisers, and compliance for regulators. These values will drive the requirements that we end up defining for our system.

Once we have completed the emprical and value investigation of informed consent, that is, identified direct and indirect stakeholders and resolved the value tensions involved, we can think about how to implement it
given our technical constraints. This is where we translate our analysis into user stories and conditions of satisfaction (see Examples section). Before we see how to do this let's take a detour and understand the structural constraints (or grammar) of defining user stories and conditions of satisfactions. 

# User Stories and Conditions of Satisfaction

A user story is an informal, general explanation of a software feature written from the perspective of the identified **stakeholders**. A user story is always of the following form:

As a <code>&lt;staekholder&gt;</code> I can <code>&lt;perform action&gt;</code> so that I can <code>&lt;receive benefit&gt;</code>

User stories represent something the stakeholder might want. There will be many ways to give them the benefit that they want.

We need to refine these in order to determine what to build. We call these refinements “conditions of satisfaction” (COS)

A COS should be a specific capability or behavior that the stakeholder expects, in the stakeholder’s terms.  It should be visible to and verifiable by the stakeholder.

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

# VSD, User Stories and Test-Driven Development

We model the development process as a cycle of refinements:

1. VSD analysis to gather requirements
2. User Stories to docoument gathered requirements
3. Conditions of Satisfaction to refine the user stories
4. Testable behaviors
5. Executable Tests
6. Engineering Tasks (Code)

As we proceed down these refinements, we will likely go back and revisit design decisions that we made at earlier stages. This is the topic of Module 02.

# Examples

## User Stories Without VSD

The following user stories were defined without performing VSD analysis.

### User Story #1

As a user of stack overflow, I want to be able to reply to questions with answers so that I can help others with my knowledge. (Essential)

### User Story #2

As a user of stack overflow, I want to list my replies and how often they are upvoted so that I can see how well people react to my answers.  (Desirable)

### User Story #3

As a user of stack overflow, I want to be able to play the codel (like the wordle but for code) so that I can enjoy my time on the site. (Extension)

## Informed Consent User Stories (Using VSD)

Based on the VSD analysis for informed consent we had resolved several value tensions and had identified the relevant stakeholders and values. We will use the observations from the analysis to document the following user stories:

### User Story #1 

As a Stack Overflow user, I want to clearly understand what personal data Stack Overflow collects through cookies and control which cookies are set so that I can make an informed choice about my privacy while still accessing the programming help I need. (Essential)

### User Story #2

As a Stack Overflow site owner, I want to implement transparent cookie consent processes that comply with regulations while maintaining user engagement so that I can build user trust, avoid legal penalties, and sustain my business model without losing essential functionality. (Essential)

### User Story #3

As an advertiser partnering with Stack Overflow, I want to access consented user data through cookies for targeted advertising so that I can deliver relevant ads to developers while respecting users' informed consent choices and maintaining advertising effectiveness. (Essential)

### User Story #4

As a regulator, I want to verify that Stack Overflow's cookie implementation provides genuine informed consent so that I can ensure user rights are protected and the platform complies with data protection laws. (Essential)

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

### For Informed Consent User Story #1

* The system should display a clear cookie banner explaining what personal data is collected before any cookies are set (Essential)
* Users should be able to access granular cookie controls to accept/reject specific categories (functional, analytics, advertising, personalization) (Desirable)
* The system should provide a "privacy dashboard" showing what data has been collected about the user over time (Extension)

### For Informed Consent User Story #2

* Cookie data containing personal information should be encrypted both in transit and at rest to prevent unauthorized access. (Essential)
* The system should automatically expire cookies based on predefined retention periods. (Essential)
* The system should allow users to read and search posts even if they reject data collection on cookies. (Desirable)
* The platform should implement automated data retention policies that permanently delete expired cookie data. (Extension)

### For Informed Consent User Story #3
* The system should only share personal data with advertisers when users have explicitly consented to advertising cookies. (Essential)
* The system should make data sharing policies explicitly available to advertising partners. (Desirable)
* The platform should provide advertisers with aggregated insights about consent patterns while preserving individual user privacy. (Extension)

### For Informed Consent User Story #4
* The system should maintain audit logs of user consent choices and consent withdrawal actions. (Essential)
* The system should provide summary reports demonstrating adherence to informed consent principles upon request. (Desirable)
* The system should provide automated tools which regulators can use to verify if the personal data collection methods comply with local data protection laws. (Extension)

Note how the user stories that resulted from VSD analysis on informed consent are markedly different from the user stories without VSD analysis -- (1) they include more stakeholders as we explicitly reasoned about them, and (2) they explicitly encompass the values we considered were important to include in our requirements. This illustrates how combining VSD analysis with user stories not only helps us think about requirements more wholistically but also document them and track them systematically. 

[User Stories](https://www.simplilearn.com/tutorials/agile-scrum-tutorial/user-stories#how_to_write_user_stories)
[VSD](https://vsd.ccs.neu.edu/introduction/what-is-vsd/)