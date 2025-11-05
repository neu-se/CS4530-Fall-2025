---
layout: page
title: Project Final Deliverable
permalink: /assignments/project-deliverable
parent: Assignments
nav_order: 6
---
# Project: Final Deliverable **Due Tuesday 11/25/2025 12pm (noon) ET**{: .label .label-red }
The final project deliverable is the implementation, available in github and deployed on render.com, and the documentation turned in to Canvas. It also includes poster and/or demos. 

## Project Implementation and Documentation
Your final team deliverable will be a "release" of your new feature on GitHub (with tests), and will be accompanied by a demo. You will submit the link of your hosted app on Canvas.

### Contents

Your final team deliverable will include:
* The implementation of your new features, deployed to Render.com / Heroku 
* Automated tests for your new features
* A continuous integration (CI) pipeline
* Project Plan as GitHub Projects
* A report that describes how to use your new feature and what was completed vs proposed
* A poster and/or demo
    
Accompanying the final team deliverable will be an *individual reflection*, which every student must submit on their own which will include your reflections on the evolution of your project concept, on the software engineering processes you used, and on your team's dynamics and collaboration.


### Submission Instructions

#### Code, documentation and Link
 All apps will be deployed on Render/Heroku (instructions for CI/CD pipeline setup are provided separately). After you have pushed all of your code (and documentation) to your team's GitHub repository, create [a release](https://docs.github.com/en/free-pro-team@latest/github/administering-a-repository/managing-releases-in-a-repository) on GitHub, and apply the tag version `final-submission`. After your release is created, you'll find that there is now a `.zip` that can be downloaded from GitHub that contains a snapshot of your entire repository. Download this zip file, unpack it, and follow the instructions that you provided in your README to double-check that the course staff will be able to run your project (this step is handy to make sure that you didn't forget to include some key files in git). If needed, you can delete the release, make some changes, and re-release up until the deadline. **Rename your zip file to include your group number in the file name. Submit this zip file to Canvas** under the assignment "Project: Code Submission" along with **the link of your hosted app** (in comments or a text file). Submit your report separately to Canvas, under the assignment "Project: Report".

#### Continuous Integration Pipeline

In your team's repo on GitHub you must have a CI workflow with the following characteristics: 
- Runs when code is integrated to a mainline branch
- Includes style checks
- Runs all automated unit tests
- Runs e2e tests for the most high value interactions in your application
- Provides quick feedback
- Is repeatable and deterministic
We will provide instructions for CI/CD pipeline setup separately.

#### Project Plan on GitHub

In your team's repo on GitHub you must have a [GitHub Project](https://docs.github.com/en/issues/planning-and-tracking-with-projects/creating-projects/creating-a-project) with a list of tasks created and completed. Each task must be linked to an issue on GitHub. Resolved issues must be connected to a commit id that was responsible for resolving it. Use of other project management tools (e.g., JIRA, Trello, notion) is not required but teams are welcome to use them **in addition** to github Projects.

#### Project Poster
Each team **MUST** submit a poster. Your poster will be a single-page PDF document, that will include the following aspects:

* Short description of the project (OK to reuse text from the project plan/report)
* Link to public demo site, link to source repo (OK to make the repo public now, or OK to leave as private)
* Short description of the technology stack and overall design decisions
* Short description of future work that could build on your project - additional features that you think could be interesting, or ideas for refactoring the code.
* Screenshots of the feature, visually demonstrating the main functionality that you implemented.

We've created a [sample poster for the "Conversation Areas" feature of Covey.Town]({{ site.baseurl }}{% link Examples/conversation-areas-poster.pdf %}), which you might find useful in deciding how to format your poster. It's fine to use a different aspect ratio (e.g. portrait instead of landscape), and there are no specific requirements for font size or amount of text. Please try to create a document that you feel represents your project, imagine your target audience as a recruiter for a software engineering role: your goal is to demonstrate that you have some experience working on some non-trivial software engineering project. **Each Poster must include your group number, names of team members and click-able links to your project repo and hosted app**. Create a PDF of your poster and rename it to include your project name and group number. A physical poster (or printed version) is not needed. **Posters will be submitted on Canvas**, under the assignment "Project: Poster / Demo".

#### Project Demo/Presentation
In addition to the poster, some sections will have live (in-person) presentations or demos. Details for project demos or presentations are provided separately by each instructor on the grading rubric page (and may vary from section to section). **Copies of presentations used in demos will be submitted on Canvas**, under the assignment "Project: Poster / Demo" (if required by your instructor).

#### Project Showcase
We will create a project showcase page for this semester (similar to the one from [Spring 2025](https://neu-se.github.io/CS4530-Spring-2025/assignments/project-showcase) semester). You will be asked to indicate your preference (if you don't want your project to be posted there) by completing a survey (a link will be provided in Canvas assignment "Project: Withdraw Permission for Showcase Page"). By default all projects will be posted unless your preference says otherwise. We often direct recruiters to that page. 
 
#### Individual Reflection
Create a PDF of your reflection, and submit it to Canvas, under the assignment "Project: Individual Reflection". 

#### Deadlines
Here are the deadlines for all of the project deliverables:
* Final Implementation (deployed site and code with all tests): Tue Nov 25th at Noon EST
* Final Report: Tue Nov 25th at Noon EST
* Poster: The last day of your section's demos/presentations
* Copy of Presentation/Demo: The last day of your section's demos/presentations 
* Individual Reflection: Mon Dec 8th at Noon EST

**Please note that the filenames for any group submission must include your group number (e.g., project_report_group101_SomeProjectName.pdf).**

## Grading
Details on grading may be found at [Project Grading]({{ site.baseurl }}{% link Assignments/project-grading.md %})