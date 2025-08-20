---
layout: assignment
title: "Individual Project 1"
permalink: /assignments/ip1
parent: Assignments
nav_order: 1
due_date: "Wednesday September 17, 2025 12:00pm EST (Noon)"
submission_notes: Submit through Github Classroom
---

Welcome aboard to the FakeStackOverflow team! We're glad that you're here and ready to join our development team as a new software engineer.
We're building an interactive application for an online community to share their knowledge and experience, and are very happy to see that we have so many new developers who can help make this application a reality.
By the end of the semester, you'll be able to propose, design, implement, and test new features for our project.
We understand that some of you may have some web development experience, but don't expect that most of you do, and hence, we have created an individual project to help you get up to speed with our existing codebase and development environment.

FakeStackOverFlow is a web application that consists of some code that runs in each client's web browser, and also code that runs on a server.

This implementation effort will be split across two deliverables. In this first deliverable, you will implement and test the core backend components for this feature, and in the second deliverable, you will implement and test the frontend components.

## Change Log
- NA

## Objectives of this assignment

The objectives of this assignment are to:

- Get you familiar with the basics of TypeScript, VSCode, and the project codebase
- Learn how to read and write code in TypeScript
- Translate high-level requirements into code
- Learn how to write unit tests with Jest

## Getting started with this assignment

Start by accepting our invitation. It will create a Github repository for you which will include the starter code for this assignment. In case you have enrolled in the course recently, you may not find your name in the list. Please create a piazza post to contact us and we will add you to the Github Classroom roster.

If you are new to Git, you may want to review the getting started page available in your project repository (look for "The Basics of GitHub.md")!

### 1. Prerequisites

#### 1.1 Install Node.js and npm

If you haven't installed npm and node.js, follow the tutorial on setting up a development environment for this class

#### 1.2 Install MongoDB

We use MongoDB as the NoSQL database to store data related to this application.

1. Follow the [instructions in the official MongoDB documentation](https://www.mongodb.com/docs/manual/administration/install-community/) to install the free community edition.
2. Choose 'Install on Linux', 'Install on macOS', or 'Install on Windows', depending on your system. (the following steps are for Windows)
3. Scroll down to the section labeled 'Install MongoDB Community Edition.' and click on [MongoDB Download Center](https://www.mongodb.com/try/download/community?tck=docs_server).
4. For Windows, in the Package dropdown, select `msi`. Then download and run the installer.
5. On Windows, select the _“Install MongoDB as a Service”_ checkbox and install. This will start MongoDB as a background service.
6. Install "MongoDB Compass" if prompted.
7. Verify if the MongoDB server is running using the Windows Services app.

Mongo offers several methods of interacting with your Mongo databases.

- MongoDB Compass is an interactive application for creating, modifying, and querying MongoDB connections. It should be started as part of the installation process, showing a connection to `mongodb://localhost:27017/`.

  For Windows, install MongoDB Compass using the instructions above.

  For Mac:

  - Download the dmg file from https://www.mongodb.com/try/download/compass. Once the application starts:
    1.  Click on "Add new connection" in the left sidebar.
    2.  Make sure the URI field contains `mongodb://localhost:27017`
    3.  Click on "Connect" - MongoDB will need to be running as a macOS service

- Mongo shell (_mongosh_) provides a command-line interface that can be used to interact with databases in MongoDB.

  For Windows:

  - Download it [here](https://www.mongodb.com/try/download/shell) using the msi package. You can also use _mongosh_ to see if the MongoDB server is running. Try the MongoDB Community Edition and the command `show dbs`; you should see a list of existing databases in your local instance.

  For Mac:

  - Mongo shell is automatically installed with MongoDB through the Mac installation instructions. To use it, make sure MongoDB is running as a macOS service, then type `mongosh` into the terminal.

- Last and most important, you can use the [Mongoose api](https://mongoosejs.com/docs/index.html) to interact with MongoDB through your JavaScript or TypeScript programs. Mongoose will be installed as part of the installation process for the project starter code.

### 2. Install the starter code and its dependencies

The starter code package, of which this is a part, is divided into 3 main directories: _client_, _server_, and _testing_.

1. Navigate to the root directory of the repo.
2. Install the dependencies for each directory by running the following commands:

```shell
cd client/
npm install
cd ../server
npm install
cd ../testing
npm install
```

Once you install the dependencies, you might see the following ESlint errors in some files. The linter error indicates that the code contains carriage return characters (\r, represented as ␍) at the end of each line and usually happens when the file has Windows-style line endings (\r\n) instead of Unix-style line endings (\n). To fix this, you can click on the "CRLF" icon on the lower right corner of VSCode and change it to "LF". Note that this does not count as a linting error when grading.
![image]({{site.baseurl}}{% link /Assignments/ip1/linter-errors.png %})

### 3. Setup Environment Variables\*\*

1. Create a file called `.env` in `./client`. In `./client/.env` ensure the following lines:

```
REACT_APP_SERVER_URL=http://localhost:8000
```

2. Create a file called `.env` in `./server`. In `./server/.env` ensure the following lines:

```
MONGODB_URI=mongodb://127.0.0.1:27017
CLIENT_URL=http://localhost:3000
PORT=8000
```

### 4. Populate the initial database

{: .note }
Right now, you may run into errors regarding unknown properties. Once you finish implementing both Task 1 and 2 and modify the schema, you should be able to populate the database correctly.

1. In the `server` directory, run `npm run populate-db` to populate the `fake_so` database with example data that follows the schema definition.
2. If you want to delete all the data at any point, you can use `npm run delete-db` to delete all entries in the `fake_so` database.

### 5. Familiarize Yourself with Project Dependencies

1. Ensure the following packages are installed: mongoose, express, jest, eslint, axios, cors, and nodemon.
2. Refer to the documentation for the following packages:

- [Express](https://expressjs.com/) is a framework to write server-side code.

- The [mongoose data modeling library](https://mongoosejs.com/docs/index.html). Mongoose provides JS/TS bindings to MongoDB, so we can manage and manipulate the data from our JS/TS programs.
- [nodemon](https://www.npmjs.com/package/nodemon) accelerates the development by automatically restarting a node application when file changes in the directory are detected.
- We use the [axios](https://axios-http.com/docs/intro) library to send HTTP requests to our server from our client application.

- We use [cors](https://www.npmjs.com/package/cors) to regulate the permissible connections between the
  clients and the server. The current cors configuration allows all
  connections to the server for convenience. This is fine for a development environment. In a
  production environment where the application is deployed on a cloud service, the CORS policy needs to be specified more strictly. Read more about CORS [https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS).

- We use [mockingoose](https://github.com/alonronin/mockingoose) to mock Mongoose functions when testing.

### 6. Explore Useful Resources

1. Express Tutorial: [https://expressjs.com/en/guide/routing.html](https://expressjs.com/en/guide/routing.html)
2. MongoDB tutorial: A mini tutorial
3. Mongoose Queries: [https://mongoosejs.com/docs/queries.html](https://mongoosejs.com/docs/queries.html)
4. Mongoose Documents: [https://mongoosejs.com/docs/documents.html](https://mongoosejs.com/docs/documents.html)
5. Jest Basics: [https://jestjs.io/docs/getting-started](https://jestjs.io/docs/getting-started)
6. Mocking in Jest: [https://jestjs.io/docs/mock-functions](https://jestjs.io/docs/mock-functions)
7. Mocking Mongoose functions: [https://github.com/alonronin/mockingoose](https://github.com/alonronin/mockingoose)
8. Postman tutorial: API Requests & Postman tutorial

## Server/Client Architecture

The schemas for the database are documented in the directory `server/models/schema`.
A class diagram for the schema definition is
shown below:

![image]({{site.baseurl}}{% link /Assignments/ip1/class-diagram.png %})

The starter code package, of which this is a part, is divided into 3 main directories: _client_, _server_, and _testing_.

### Client

Running `npm run start` will start a client on port 3000.
The client code uses Axios to send HTTP method requests to the server. You should review the client code to understand
how axios sends requests and how the response from the server is processed. You don’t need to make any changes to the client code.

### Server

The server is responsible for taking HTTP requests from the client and executing them on the database. The server code resides in the `server/` directory. The server is responsible for all the data that is sent back and forth to the database.

The main server script is in `server/server.ts`. Running `npm run start`
will start an HTTP server, which will take HTTP requests on [**https://localhost:8000**](https://localhost:8000/), and execute them on the running database instance.

You can send requests to the server using a tool like Postman, or by writing scripts that use axios to send requests to `localhost:8000`, as you did in the Async activity.

When the server is terminated (using CTRL+C), the message **“Server closed.”** should be displayed. However, the MongoDB service will still be running (You can run `mongosh` to confirm)

### Testing

Unit tests for the server are in `server/tests/*/*.spec.ts`. These are written in Jest, which you are already familiar with.

To run the entire set of server tests, go to the server directory and say `npm run test`. Please ensure that the MongoDB server is up and running for the tests to pass.

If you want to run specific tests, we recommend that you install vsc-jest-runner in your VSC, and select the test or tests that you would like to run.

### Summary of the default host/port settings

|                   |                                                                        |
| :---------------- | :--------------------------------------------------------------------- |
| Client Instance   | [https://localhost:3000/](https://localhost:3000/)                     |
| Server Instance   | [https://localhost:8000/](https://localhost:8000/)                     |
| Database Instance | [mongodb://127.0.0.1:27017/fake_so](mongodb://127.0.0.1:27017/fake_so) |

## Recommendations when working on the project

1. Open the client application in a browser and interact with it. While interacting, monitor
   the application tab in the browser’s developer tools. The application tab will give you
   information about the HTTP requests the client sends to the server. The HTTP requests
   will contain URIs in their headers. You can use this information to understand the
   endpoints in the server.
2. Read the Jest tests. The Jest tests list all the endpoints the server should have, and the
   types of HTTP method associated with them. Further, the tests also have information
   about the Mongoose functions that need to be invoked for the service to send a
   successful response.
3. Start by defining the schemas in the server/models/schema directory to ensure the data structure is consistent.
4. Ensure that you run all Jest tests. These tests are designed to catch issues early. Once all Jest tests pass, the Cypress tests should also pass, assuming no significant changes have been made to the client’s implementation.
5. Use Postman to interact with and manually test your solutions and verify that database queries work as expected.
6. Follow the [debugging policy](https://neu-se.github.io/CS4530-Fall-2025/policies/debugging/) to help in the debugging process.

## Implementation Tasks

This deliverable has 2 parts; each part will be graded on its own rubric. 

### Task 1: Collection

A collection is a curated set of questions related to a specific topic or theme. Users of the website should be able to do the following:

1. Create a new collection.
2. Delete an existing collection.
3. Create a new question in an existing collection.
3. Retrieve a collection by Id
5. Retrieve all collections by the username of the user that created them.

#### Steps to Achieve This

1. Create the Mongoose schema for collection

    The collection schema defines the structure for storing a collection document in the MongoDB database. Each collection must have the following:

    - a __name__ of type string. This is required.
    - an optional __description__ of type string.
    - a list of __questions__ associated with the collection. An empty list denotes the collection has no questions yet.
    - a required __username__ of type string of the user that created the collection.
    - a boolean property __isPrivate__ to denote if the collection is private to the user that created it or if it can be used by other users. A collection is private by default.

    Define the schema in `server/models/schema/collection.schema.ts`. You can verify the schema by running the scripts described in Section 4 of this document.
2. Define a Mongoose model for collection

    Mongoose requires us to construct a data layer object from a given schema. The data layer object serves as the interface to the database. To this end, define the collection model in `server/models/collection.model.ts`. 
3. Define relevant types

    Define the relevant types needed for the collections feature in `server/types/types.d.ts` as marked by *TODO: Task 1*. Be sure to avoid repeated or reduntant type definitions.
4. Implement the service layer functions

    The role of the service layer functions is to interact with the data layer object and the controllers. To this end, define the following functions in `server/services/collection.service.ts`:

    - `createCollection(collection)` creates a new collection in the database if the collection does not exist.
    - `deleteCollection(id, username)` removes a collection in the database with the given id and crated by a user with the given username. It returns the deleted collection if successful, otherwise throws an error.
    - `getCollectionByUsername(username, currentUsername)` returns all collections stored in the databse for a given username. If the given username is not the same as the current user making the request then the private collections must not be returned. Throws an error if the relevant collections cannot be retrieved.
    - `getCollectionById(id, username)` returns the collection for a given collection ID and created by a user with the username. Throws an error if the collection cannot be retrieved or a private collection is being requested by a user who did not create it.
    - `addQuestionToCollection(id, questionId, username)` adds a question with a question ID to an existing collection with a given ID and username. If the question being added then removes the question and updates the collection, otherwise creates a new question with the given ID and updates the collection. In either case it returns the updated collection. Throws an error if the collection does not exist or could not be updated.

5. Define the endpoints

    Define the following express REST API endpoints in `server/controller/collection.controller.ts`:

    - `createCollectionRoute(req, res)` takes an HTTP request containing the metadata in its body necessary to create a collection and creates a collection. It returns the created collection as reponse.
    - `deleteCollectionRoute(req, res)` takes an HTTP request containing a collection ID and the username of the collection and deletes the corresponding collection. It returns the deleted collection as response of the delete was successful.
    - `toggleSaveQuestionRoute(req, res)` takes an HTTP request with the question ID that needs to be saved and the collection ID where the question will be a part of. It returns the updated collection as response.
    - `getCollectionsByUsernameRoute(req, res)` takes an HTTP request containing the username of the currenly logged in user and the username of some other user. It returns all collections for the username as response.
    - `getCollectionByIdRoute(req, res)` takes an HTTP request containing the collection ID and the username of the user that created the collection. It returns the corresponding collection as response.

    All endpoints return a status code of 200 in their response. However, in case of an error they return a status code 50 in their response and in case of an invalid request they return a status code of 400 in their reponse.
6. Add routes to endpoints

    Define the appropriate API routes on the Express router for each of the functions implemented in the previous steps.
7. Document endpoints as Open API spec (tentative)

    Write JSDoc comments for every endpoint to generate an OpenAPI spec for them.
8. Write unit tests

    We’ve provided initial tests to provide some information on the expected behavior of the routes and functions. Using the requirement descriptions above, write additional tests for all the added functions and routes, covering different branches, edge cases, etc. to verify the correctness of your code.

    Add your unit tests to the file `server/tests/services/collection.service.spec.ts` and `server/tests/controllers/collection.controller.spec.ts`

    In addition to automated tests, you should also manually test your route using Postman and MongoDB Compass to ensure that any database queries are correct since we use database mocks while testing with Jest.

#### Grading (X points)

- Schema and data model = 5 points
- Types = 5 points
- Service layer Implementation = 20 points
- Endpoint integration = 10 points
- Open API Spec = 5 points
- Testing = 20 points
  - 2 points for each function

### Task 2: Communities

A community is a subgroup of users with common interests. A community can be public or private. A public community is open to all users of the platform. On the other hand a private community is only accessible to its members. A community always has an admin selected from its participants/members. Extend the current implementation with the following features:

  1. Retrieve details of an existing community
  2. Retrieve details of all communities
  3. Join/leave a community
  4. Create a new community
  5. Delete an existing community

#### Steps to Achieve This

1. Create the schema

    The community schema defines the structure of a document in the community collection of the MongoDB database. Each community must have the following:

    - A required unique __name__ of type string.
    - A required __description__ of type string.
    - A list of __participants__ in the community.
    - A __visibility__ type for the community -- always must be public or private. The default visibility of a community is public.
    - a required __admin__ user of type string.

    Define the schema in `server/models/schema/community.schema.ts`.

    Make sure the Questions schema structure in `server/models/schema/question.schema.ts` has a reference to an existing `community`.

    You can verify the schema by running the scripts described in Section 4 of this document.

2. Define the mongoose model

    Mongoose requires us to construct a data layer object from a given schema. The data layer object serves as the interface to the database. To this end, define the community model in `server/models/community.model.ts`.

3. Define the relevant types

    Define the relevant types needed for the communities feature in `server/types/types.d.ts` as marked by TODO: Task 2. Be sure to avoid repeated or reduntant type definitions.

4. Implement the service Layer functions

    Define the following functions in `server/services/community.service.ts`:

    - `getCommunity(id)` returns an object based on the document in the community collection for an existing community ID. It returns an object with an error property if it fails to retreive the document.

    - `getAllCommunities()` returns all communities in the community collection in the database. It returns an object with the error property if the retrieval fails.

    - `toggleCommunityMembership(id, username)` takes a community ID and a username and adds the user with the given username as a participant to the community with the given ID if the user is not a participant. If the user is a participant but not an admin in the community then it removes them from the community. It returns an object with the error property if the update to the relevant document fails.

    - `createCommunity(community)` creates a new community in the database with the given community data and returns the newyly created community. It returns an object with the error property if the creation fails.

    - `deleteCommunity(id, username)` deletes an existing community with the given id from the database when requested by a user with the given username and if the user is an admin. It returns an object with the error property if deletion fails or the user is not an admin of the communnity.

5. Define the endpoints

    - `getCommunityRoute(req, res)` takes an HTTP request that contains a community ID and returns the found community as response.

    - `getAllCommunitiesRoute(req, res)` takes an HTTP request and returns all communities as response. 

    - `toggleMembershipRoute(req, res)` takes an HTTP request containing the username of the user that wants to leave/join a community with an ID. It returns the updated community object as response. 

    - `createCommunityRoute(req, res)` takes an HTTP request containing the necessary metadata needed to create a community and returns the newly created community as response. 

    - `deleteCommunityRoute(req, res)` takes an HTTP request containing the username of the user requesting the delete and the community ID that needs to be deleted. It returns the deleted community as response. 

6. Add routes to endpoints

    Define the appropriate API routes on the Express router for each of the functions implemented in the previous steps.

7. Document endpoints as Open API spec (tentative)

    Write JSDoc comments for every endpoint to generate an OpenAPI spec for them.
8. Write unit tests

    We’ve provided initial tests to provide some information on the expected behavior of the routes and functions. Using the requirement descriptions above, write additional tests for all the added functions and routes, covering different branches, edge cases, etc. to verify the correctness of your code.

    Add your unit tests to the file `server/tests/services/community.service.spec.ts` and `server/tests/controllers/community.controller.spec.ts`

    In addition to automated tests, you should also manually test your route using Postman and MongoDB Compass to ensure that any database queries are correct since we use database mocks while testing with Jest.

## Submission Instructions & Grading

You will submit your assignment using GitHub Classroom.

This submission will be scored out of 100 points, 90 of which will be awarded for implementation of tasks and accompanying tests, and the remaining 10 for following style guidelines.

Your code will automatically be evaluated for linter errors and warnings.

- Each lint error or warning will result in a deduction of -2 points (up to a maximum of 30 points).
- This will not affect the 10 style points.
- Line endings will not be counted as errors.

The starter code comes with some lint problems, You are expected you to fix these linter problems, many of them will be fixed as you implement the tasks.

**The use of `eslint-disable` statements is NOT allowed. Each instance outside what is provided in the starter code will have points deducted.**

You can run the following command within the client or server to fix some common lint errors

```
npm run lint:fix
```

#### Testing

You will be provided with starter code that includes a set of tests. Your task is to ensure that all existing tests pass and to create additional tests to cover any new functionality or edge cases.

### Manual Grading

Your code will be manually evaluated for conformance to our [course style guide](https://neu-se.github.io/CS4530-Fall-2025/policies/style/). **Do not wait to run the linter until the last minute**. To check for linter errors, run the command `npm run lint` from the terminal. The handout contains the same ESlint configuration that is used by our grading script.

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

> {: .note }
> Please update the node version used in the github action workflow to be `22.x` instead of `20.x`. This will fix any memory leaks errors raised while executing the test suite. In particular, change lines 23-26 of `.github/workflows/main.yml` to be:

```yml
- name: Set up Node.js 22.x
  uses: actions/setup-node@v4
  with:
    node-version: "22.x"
```

#### Debugging

If you need help troubleshooting a problem, be sure to follow all the steps outlined in the course's [debugging policy]({{ site.baseurl }}{% link debugging.md %}). This will ensure you have exhausted all initial debugging strategies before reaching out for assistance from the TAs.

### Academic Integrity

Please refer to the [course policy page](https://neu-se.github.io/CS4530-Fall-2025/policies/#academic-integrity) for more details.

**For this assignment, the use of co-pilot or other generative AI technologies such as ChatGPT is not allowed.**


```
