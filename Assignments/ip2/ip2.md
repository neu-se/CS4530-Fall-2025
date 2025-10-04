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

- 2024-10-03: Updated descriptions for useAllCommunitiesPage and useCommunityCard hooks to clarify functionality and access restrictions.
- 2024-09-30: Fixed changeCommunityMembership  implementation description to correctly reflect the use of POST request. Added note to create a button to open the modal to save a question to an existing collection.
- 2024-09-27: Added new task under Collections implementation to verify sidebar navigation route setup.
- 2024-09-21: 1. Removed Note on the Server tests will fail.2. All sections that say “Complete the component defined in that directory” in collections have been removed.3. Implement community service functions now has the same level of detail as Implement collection service functions.4. Corrected service function names in community service functions.5. Added comprehensive Cypress testing section.


## Objectives of this assignment

The objectives of this assignment are to:

- Investigate and understand a large, existing codebase
- Implement interaction-level design using:
  - asynchronous programming constructs
  - the React library
- (Optional). Learn to comprehend and work with larger scope tests.

## Getting started with this assignment

Start by accepting our [invitation](https://classroom.github.com/a/HTonpwlZ). It will create a Github repository for you which will include the starter code for this assignment. Run `npm install` in the root directory to fetch all dependencies for the `client`, `server`, and `shared` folders. You should not install any additional dependencies: **'package.json' must be unchanged**. You should also not delete the **package-lock.json** file.

{: .note }
**Note:** You may see warnings about vulnerabilities after running npm install. These should be ignored. Do NOT run `npm audit fix` or `npm audit fix --force` as this will change your package-lock.json file. 

{: .note }
Refer to [IP1](https://neu-se.github.io/CS4530-Fall-2025/assignments/ip1) for instructions related to setting up MongoDB, setting environment variables, and running the client and server.

{: .note }
**System-level dependencies:** The libraries used for React require some native binaries to be installed -- code written and compiled for your computer (not JavaScript). If you run into issues with `npm install` not succeeding, please try installing the following libraries using either [Homebrew (if on Mac)](https://brew.sh), apt-get, or your favorite other package manager: `pixman`, `cairo`, `pkgconfig` and `pango`. For example, on a Mac, after installing Homebrew, run `brew install pixman cairo pkgconfig pango`. **You should not continue with the installation until this succeeds.** On Windows: Students have reported seeing the failure `error /bin/bash: node: command not found` upon `npm install` in the `client` directory. If you encounter this error, please try to delete the `node_modules` directory and re-run `npm install` in the `client` directory from a bash shell instead of a windows command prompt.

These are some convenience scripts that you can use while working on the assignment:

1. `npm run dev` (client + server) - This can be used to start the client or server in the respective directory the command is run. Both the client and server will reload every time a file is saved, reflecting any changes live.
2. `npm run debug-test` (server)- This runs the test command with coverage.
3. `npm run lint` (client + server) - This can be used check style errors in both client and server. Note the client starter code has lint errors you are expected to fix. Don't fix them immediately as some of the errors are due to hints provided in the starter code, which will be helpful to complete the implementation tasks. In fact, you can run lint to and inspect the errors to figure out the hints.
4. Make you sure the MongoDB process `mongod` is running. You can check this by running `mongosh`. If this isn't running then the client won't be able to connect to the database through the server.

## Implementation Tasks

This deliverable has 2 parts; each part will be graded by its own rubric provided in the "Grading" section. You're recommended to complete this assignment one task at a time, in the order provided. For this assignment, follow test-driven development (TDD). Read the tests in the server to understand how the server endpoints are expected to behave and use that understanding to inform the implementation of the client. Do **not** change the provided server tests to match your implmentation. The repository README also documents the server endpoints.

The client implementation has a service layer in `services`. Review the existing code in that layer to understand how the 
client interacts with the server endpoints. You will need to create your own client service for the implementation tasks.

### Task 1: Collections Frontend Implementation (90 points)

In IP1, you implemented the backend functionality for Collections. In this task, you will build the frontend components to allow users to interact with collections through the user interface.

#### Steps to Achieve This

##### In Client


**Create `useAllCollectionsPage` custom hook**

Create a new file `./client/src/hooks/useAllCollectionsPage.ts`. In this file, you will implement the `useAllCollectionsPage` custom hook, which manages the state and logic for displaying all collections belonging to a user. The hook should fetch collections when the component mounts using the `getCollectionsByUsername` service function and handle loading states.

**Complete the `AllCollectionsPage` component**

Update the component to use the `useAllCollectionsPage` hook. Implement state management using the `useAllCollectionsPage` hook. Use the returned values from the hook to display the collections list.

**Create `useCollectionPage` custom hook**

Create a new file `./client/src/hooks/useCollectionPage.ts`. This hook manages the state for viewing a single collection, including fetching the collection details by ID and handling real-time updates via socket events sent from the server.

**Complete the `CollectionPage` component**

Use the `useCollectionPage` hook for state management.

**Create `useDeleteCollectionButton` custom hook**

Create a new file `./client/src/hooks/useDeleteCollectionButton.ts`. Implement logic for deleting a collection with confirmation handling.

**Complete the `DeleteCollectionButton` component**

In `./client/src/components/main/collections/deleteCollectionButton/index.tsx`, create a button component that handles collection deletion. Use the `useDeleteCollectionButton` hook for the deletion logic.

**Create `useNewCollectionPage` custom hook**

Create a new file `./client/src/hooks/useNewCollectionPage.ts`. Implement the hook to manage form state for creating a new collection. The `postCollection` function should validate inputs and submit using the `createCollection` service.

**Complete the `NewCollectionPage` component**

In `./client/src/components/main/collections/newCollectionPage/index.tsx`, create the form for adding a new collection. Use the `useNewCollectionPage` hook. Implement state management using the `useNewCollectionPage` hook.

**Create `useSaveToCollectionModal` custom hook**

Create a new file `./client/src/hooks/useSaveToCollectionModal.ts`. This hook manages the modal state for saving questions to collections, including fetching user collections and toggling question membership.

**Complete the `SaveToCollectionModal` component**

In `./client/src/components/main/collections/saveToCollectionModal/index.tsx`, implement the modal that allows users to save/unsave questions to their collections. Display checkboxes for each collection showing current save status.

**Update the menu in the sidebar to render collection of a username**

Review the code in `src/components/main/sideBarNav/index.tsx`. Verify that the route for collections is setup correctly to render the collections for a particular username.

**Implement collection service functions**

In `./client/src/services/collectionService.ts`, implement the following service functions:

- `getAllCollectionsByUsername`: Fetches all collections for a user
  - The getAllCollectionsByUsername function retrieves all collections for a specific user with proper authorization. Make a GET request using api.get(). The usernameToView is a path parameter, while currentUsername is a query parameter for permissions. Check for status 200 and throw "Error while fetching all collections" if it fails. Return res.data, containing an array of PopulatedDatabaseCollection objects.

- `getCollectionById`: Fetches a single collection by ID
  - The getCollectionById function fetches a single collection by ID with user authorization. Use api.get(), where the collectionId is specified as the path parameter and the username is included as the query parameter. Verify status 200 and throw "Error while fetching collection" on failure. Return res.data with the PopulatedDatabaseCollection object.

- `createCollection`: Creates a new collection
  - The createCollection function creates a new collection by sending a POST request with the collection object as the request body. Use api.post() to send the request and check if the response status is 200; if it is not, throw an error with the message "Error while creating collection." Return res.data containing the created collection object.

- `deleteCollection`: Deletes a collection
  - The deleteCollection function permanently removes a collection with user verification. Use api.delete() to request where both parameters are included in the URL (no request body needed). Verify status 200 and throw "Error while deleting collection" on failure. Return res.data with the deletion confirmation.

- `toggleSaveQuestion`: Adds or removes a question from a collection
  - The toggleSaveQuestion function adds or removes questions from collections using toggle logic. Send a PATCH request using api.patch(), passing { collectionId, questionId, username } as the request body. Check for status 200 and throw "Error while toggling save question" if failed. Return res.data with the operation result.


**Create a Save to an Existing Collection Button in Question Component**

In `.client/src/components/main/questionPage/question/index.tsx`, add a button that opens the modal to save a question to an existing collection.The button must have the className='collections-btn'. Clicking this button should  open the modal, which will allow the user to add a question to one of its collections.



#### Grading (90 points)

- `useAllCollectionsPage` hook = 10 points
- `AllCollectionsPage` component = 10 points
- `useCollectionPage` hook = 10 points
- `CollectionPage` component = 7 points
- `useDeleteCollectionButton` hook = 5 points
- `DeleteCollectionButton` component = 3 points
- `useNewCollectionPage` hook = 8 points
- `NewCollectionPage` component = 5 points
- `useSaveToCollectionModal` hook = 7 points
- `SaveToCollectionModal` component = 20 points
- Collection service functions = 15 points

### Task 2: Communities Frontend Implementation (90 points)

In IP1, you implemented the backend functionality for Communities. In this task, you will build the frontend components to allow users to interact with communities through the user interface.

#### Steps to Achieve This

##### In Client

**Create `useAllCommunitiesPage` custom hook**

Create a new file `./client/src/hooks/useAllCommunitiesPage.ts`. This hook manages the state for displaying all communities. It should fetch communities using the `getCommunities` service function and handle updates to existing communities.

**Complete the `AllCommunitiesPage` component**

In `./client/src/components/main/communities/allCommunitiesPage/index.tsx`, we've defined a component to display all communities. Update the component to use the `useAllCommunitiesPage` hook. Implement state management using the `useAllCommunitiesPage` hook.

**Create `useCommunityCard` custom hook**

Create a new file `./client/src/hooks/useCommunityCard.ts`. This hook manages the render logic to display all communities. Private communities cannot be viewed by non members.

**Complete the `CommunityCard` component**

In `./client/src/components/main/communities/communityCard/index.tsx`, implement the component to display community information. Use the `useCommunityCard` hook for state management.

**Create `useCommunityMembershipButton` custom hook**

Create a new file `./client/src/hooks/useCommunityMembershipButton.ts`. This hook manages the join/leave functionality for communities.

**Complete the `CommunityMembershipButton` component**

In `./client/src/components/main/communities/communityMembershipButton/index.tsx`, create a button that handles joining and leaving communities. Use the `useCommunityMembershipButton` hook.

**Create `useCommunityPage` custom hook**

Create a new file `./client/src/hooks/useCommunityPage.ts`. Implement the hook to manage state for viewing a single community, including fetching community details and handling real-time updates.

**Complete the `CommunityPage` component**

In `./client/src/components/main/communities/communityPage/index.tsx`, implement the component to display community details and members. Use the `useCommunityPage` hook.

**Create `useNewCommunityButton` custom hook**

Create a new file `./client/src/hooks/useNewCommunityButton.ts`. Implement logic for showing the new community creation button.

**Complete the `NewCommunityButton` component**

In `./client/src/components/main/communities/newCommunityButton/index.tsx`, create a button component that navigates to the new community page.

**Create `useNewCommunityPage` custom hook**

Create a new file `./client/src/hooks/useNewCommunityPage.ts`. Implement the hook to manage form state for creating communities. The `postCommunity` function should validate inputs and submit using the service.

**Complete the `NewCommunityPage` component**

In `./client/src/components/main/communities/newCommunityPage/index.tsx`, create the form for adding a new community. Use the `useNewCommunityPage` hook for state management.

**Implement community service functions**

In `./client/src/services/communityService.ts`, implement the following service functions:

- `getCommunityById`: Retrieves a single community by ID
  - The getCommunityById function fetches one community using its ID. Use api.get() with the communityId as a path parameter.Verify the response status is 200; otherwise, throw "Error while fetching community". Return res.data as a DatabaseCommunity object.
- `getCommunities`: Retrieves all communities
  - The getCommunities function returns the full list of communities. Make a GET request with api.get().Check for status 200 and throw "Error while fetching all communities" if it fails. Return res.data, which should be an array of DatabaseCommunity objects.
- `changeCommunityMembership`: Toggles user membership in a community
    - The changeCommunityMembership function adds or removes a user from a community using toggle logic. Send a POST request via api.post()  with { communityId, username } in the request body. Confirm status 200; if not, throw "Error while changing community membership". Return res.data containing the updated community.
- `createCommunity`: Creates a new community
  - The createCommunity function creates a community by sending a POST request with the new Community object as the request body using api.post() to an endpoint.Ensure the response status is 200; otherwise throw "Error while creating community". Return res.data containing the created DatabaseCommunity.
- `deleteCommunity`: Deletes a community
  - The deleteCommunity function removes a community permanently by ID. Use api.delete() with the communityId as a path parameter.Verify status 200; if it fails, throw "Error while deleting community". Return res.data with the deletion confirmation or result.

#### Points to note

- The client starter code has lint errors which you are expected to fix. They will go away when you implement the hints.
- Run the server and the client and render the client in the browser to get a sense of the user interface.
- Do not change the classNames of React components in the starter code. We will use the classNames in automated tests.

#### Grading (90 points)

- `useAllCommunitiesPage` hook = 10 points
- `AllCommunitiesPage` component = 8 points
- `useCommunityCard` hook = 4 points
- `CommunityCard` component = 5 points
- `useCommunityMembershipButton` hook = 4 points
- `CommunityMembershipButton` component = 4 points
- `useCommunityPage` hook = 8 points
- `CommunityPage` component = 12 points
- `useNewCommunityButton` hook = 3 points
- `NewCommunityButton` component = 2 points
- `useNewCommunityPage` hook = 9 points
- `NewCommunityPage` component = 6 points
- Community service functions = 15 points


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

You do not need to write automated tests for the frontend, but are encouraged to extensively manually test your implementation.
##### Cypress Tests

**Please Note -  Running Cypress tests is optional.Cypress tests requires significant system resources, and without them, the tests may be flaky. We will run similar (not the same) tests for grading.**

The Cypress tests (located in the `testing/` directory) are provided as an example of GUI and end-to-end (E2E) tests. They can be used to check the correctness of your implementation, but **you are not expected to write** Cypress tests. Please see the README for full instructions on running the Cypress tests.

##### Running the Cypress tests (optional)

These are end-to-end (E2E) tests and are provided to help validate the existing features. Follow the steps below to set up and run them.

1. Install dependencies for the tests
```bash
npm install in /testing
```
2.Create the .env file used by the tests
```bash
# in the testing/ directory create a .env file containing:
MONGODB_URI=mongodb://127.0.0.1:27017
```
3. Start the server and client
4. Open the Cypress UI
```bash
# from the testing/ directory
npx cypress open
```
5. Run tests via the Cypress UI
- choose "e2e testing", then click Start, and click any test file to run it


### Manual Grading

Your code will be manually evaluated for conformance to our [course style guide](https://neu-se.github.io/CS4530-Spring-2025/policies/style/). **Do not wait to run the linter until the last minute**. To check for linter errors, run the command `npm run lint` from the terminal. The handout contains the same ESlint configuration that is used by our grading script.

This manual evaluation will account for 10% of your total grade on this assignment. We will manually evaluate your code for style on the following rubric:

To receive all 20 points:

- All new names (e.g. for local variables, methods, and properties) follow the naming conventions defined in our style guide
- There are no unused local variables
- All public properties and methods (other than getters, setters, and constructors) are documented with JSDoc-style comments that describe what the property/method does, as defined in our style guide
- The code and tests that you write generally follows the design principles discussed in week one. In particular, your design does not have duplicated code that could have been refactored into a shared method.
- No duplicate code is allowed.

We will review your code and note each violation of this rubric. We will deduct 4 points for each violation, up to a maximum of deducting all 20 style points.

#### GitHub Actions for Test and Lint Output

Once your submission is pushed to your main branch, GitHub will automatically run linting and the tests in `server/tests` for your submission. Check the Actions tab on GitHub classroom to see the output of the run. This output will be used for grading, so ensure there are no errors in the Actions run.

![image]({{site.baseurl}}{% link /Assignments/ip1/ActionsTab.png %})


#### Debugging

If you need help troubleshooting a problem, be sure to follow all the steps outlined in the course's [debugging policy]({{ site.baseurl }}{% link debugging.md %}). This will ensure you have exhausted all initial debugging strategies before reaching out for assistance from the TAs.

### Academic Integrity

Please refer to the [course policy page](https://neu-se.github.io/CS4530-Fall-2025/policies/#academic-integrity) for more details.

**For this assignment, the use of generative AI technologies such as ChatGPT is not allowed.**