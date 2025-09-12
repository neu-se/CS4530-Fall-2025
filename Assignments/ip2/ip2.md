---
layout: assignment
title: "Individual Project 2"
permalink: /assignments/ip2
parent: Assignments
nav_order: 2
due_date: "Wednesday October 15, 2025 12:00pm EST (Noon)"
submission_notes: Submit through Github Classroom (Commit your work in main branch)
---

Welcome back to the Stack Overflow team! In this second deliverable, you will be implementing new and exciting features to enhance the frontend interface and bring the web application to life. This assignment builds on the foundation you laid in the first project and will deepen your skills in frontend development with TypeScript and React.

## Change Log

- None.

## Objectives of this assignment

The objectives of this assignment are to:

- Investigate and understand a large, existing codebase
- Write new TypeScript code that uses asynchronous operations
- Write test cases that utilize mocks and spies
- Write React components and hooks that make use of state

## Getting started with this assignment

Start by accepting our invitation. It will create a Github repository for you which will include the starter code for this assignment. Run npm install within `./client` and `./server` to fetch the dependencies. You should not install any additional dependencies: **‘package.json’ must be unchanged**.

{: .note }
Refer to [IP1](https://neu-se.github.io/CS4530-Fall-2025/assignments/ip1) for instructions related to setting up MongoDB, setting environment variables, and running the client and server.

{: .note }
**System-level dependencies:** The libraries used for React require some native binaries to be installed -- code written and compiled for your computer (not JavaScript). If you run into issues with `npm install` not succeeding, please try installing the following libraries using either [Homebrew (if on Mac)](https://brew.sh), apt-get, or your favorite other package manager: `pixman`, `cairo`, `pkgconfig` and `pango`. For example, on a Mac, after installing Homebrew, run `brew install pixman cairo pkgconfig pango`. **You should not continue with the installation until this succeeds.** On Windows: Students have reported seeing the failure `error /bin/bash: node: command not found` upon `npm install` in the `client` directory. If you encounter this error, please try to delete the `node_modules` directory and re-run `npm install` in the `client` directory from a bash shell instead of a windows command prompt.

These are some convenience scripts that you can use while working on the assignment:

1. `npm start` / `npm run start` (client + server) - This can be used to start the client or server in the respective directory the command is run. Both the client and server will reload every time a file is saved, reflecting any changes live.
2. `npm run debug-test` (server)- This runs the test command without checking for memory leaks. Often, the Jest memory leak error is introduced by failing tests, so resolving any errors should be the first step in debugging the memory leak. `npm test` / `npm run test` will be used for grading, however, so ensure your GitHub Actions workflow is passing.

## Implementation Tasks

This deliverable has 3 parts; each part will be graded by its own rubric provided in the "Grading" section. You're recommended to complete this assignment one task at a time, in the order provided. For this assignment, follow test-driven development (TDD). Read the tests to understand how the functions are expected to behave and use that understanding to inform your implementation. Do **not** change the provided tests to match your implmentation.

### Task 1: User-Related Pages

In IP1, we defined several API routes and database operations to support users on the forum. In particular, we added the following features:

1. TBA

In this task, we'll build on this to allow users to interact with it in the frontend, as well as add some additional functionality to bring our forum to life.

#### Steps to Achieve This

.....

#### Grading (56 points)

- TBA
- Testing = 6 points

### Task 2: Games

...


#### Steps to Achieve This

....

#### Grading (43 points)

....


## Submission Instructions & Grading

You will submit your assignment using GitHub Classroom. **All commits must be visible on the main branch on GitHub classroom to receive credit.**

This submission will be scored out of 200 points, 180 of which will be awarded for implementation of tasks and accompanying tests, and the remaining 20 for following style guidelines.

Your code will automatically be evaluated for linter errors and warnings.

- Each lint error or warning will result in a deduction of -2 points (up to a maximum of 30 points).
- This will not affect the 20 style points.
- Line endings will not be counted as errors.

The starter code comes with some lint problems, You are expected you to fix these linter problems, many of them will be fixed as you implement the tasks.

**The use of `eslint-disable` statements is NOT allowed. Each instance outside what is provided in the starter code will have points deducted.**

You can run the following command within the client or server to fix some common lint errors

```
npm run lint:fix
```

#### Testing

You will be provided with starter code that includes a set of tests. Your task is to ensure that all existing tests pass and to create additional tests to cover any new functionality or edge cases in the server. You do not need to write Jest tests for socket code in the server (e.g. `socket.emit` statements in `chat.controller.ts`, `joinChat`, `leaveChat` events). However, you will be able to identify if it's working correctly by interacting with the frontend client.

**Please Note**: The server tests will fail the first time students run them but this is expected behavior.Please rerun the tests after you have completed the implementation.All server tests will pass after students have implemented the features as well as the corresponding tests. Please also  take note until all tests have passed, the Github actions will fail; this is also an expected behavior.These actions will pass when 1.Community and Collection features are implemented and 2.Tests are implemented.

You do not need to write automated tests for the frontend, but are encouraged to extensively manually test your implementation.

### Manual Grading

Your code will be manually evaluated for conformance to our [course style guide](https://neu-se.github.io/CS4530-Spring-2025/policies/style/). **Do not wait to run the linter until the last minute**. To check for linter errors, run the command `npm run lint` from the terminal. The handout contains the same ESlint configuration that is used by our grading script.

This manual evaluation will account for 10% of your total grade on this assignment. We will manually evaluate your code for style on the following rubric:

To receive all 10 points:

- All new names (e.g. for local variables, methods, and properties) follow the naming conventions defined in our style guide
- There are no unused local variables
- All public properties and methods (other than getters, setters, and constructors) are documented with JSDoc-style comments that describe what the property/method does, as defined in our style guide
- The code and tests that you write generally follows the design principles discussed in week one. In particular, your design does not have duplicated code that could have been refactored into a shared method.
- No duplicate code is allowed.

We will review your code and note each violation of this rubric. We will deduct 2 points for each violation, up to a maximum of deducting all 10 style points.

#### GitHub Actions for Test and Lint Output

Once your submission is pushed to your main branch, GitHub will automatically run linting and the tests in `server/tests` for your submission. Check the Actions tab on GitHub classroom to see the output of the run. This output will be used for grading, so ensure there are no errors in the Actions run.

![image]({{site.baseurl}}{% link /Assignments/ip1/ActionsTab.png %})


#### Debugging

If you need help troubleshooting a problem, be sure to follow all the steps outlined in the course's [debugging policy]({{ site.baseurl }}{% link debugging.md %}). This will ensure you have exhausted all initial debugging strategies before reaching out for assistance from the TAs.

### Academic Integrity

Please refer to the [course policy page](https://neu-se.github.io/CS4530-Fall-2025/policies/#academic-integrity) for more details.

**For this assignment, the use of generative AI technologies such as ChatGPT is not allowed.**