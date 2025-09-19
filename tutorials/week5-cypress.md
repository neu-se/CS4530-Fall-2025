---
layout: page
title: UI Testing with Cypress
permalink: /tutorials/week5-cypress
parent: Tutorials
nav_order: 9
---
# UI Testing with Cypress

This tutorial covers the basic concepts of UI testing and end-to-end (E2E) testing using Cypress. By the end, you’ll have a clear understanding of UI testing, how it compares with other forms of testing, and how to implement Cypress for UI testing with practical examples.

## Demo Project for Practice
Before we dive into the details, you can download and set up a demo project that will help you understand Cypress testing better. This project will provide a hands-on environment where you can explore different scenarios and practice writing Cypress tests.

### 1. Download the Cypress Demo Project
Download the Cypress demo project from the link below.

[Cypress Demo](./assets/week5-cypress/cypress-demo.zip)
### 2. Install Dependencies

After downloading and extracting the ZIP file, navigate to the project directory and install the necessary dependencies using npm:

```bash
cd cypress-demo
npm install
```

### 3. Open Cypress

Once the dependencies are installed, open Cypress using the following command:

```bash
npx cypress open
```

## Contents:

- [What is UI Testing?](#what-is-ui-testing)
    - [UI Testing vs. E2E Testing](#ui-testing-vs-e2e-testing)
    - [Example Scenarios](#example-scenarios)
- [Using Cypress for UI Testing](#using-cypress-for-ui-testing)
    - [Setting Up Cypress](#setting-up-cypress)
    - [Common Commands](#common-commands)
- [Example Scenarios and Tests](#example-scenarios-and-tests)
    - [Scenario 1: Testing a Login Form](#scenario-1-testing-a-login-form)
    - [Scenario 2: Testing a Search Feature](#scenario-2-testing-a-search-feature)
    - [Scenario 3: Form Submission and Validation](#scenario-3-form-submission-and-validation)
- [Where to Place Cypress Tests](#where-to-place-cypress-tests)
- [New Cypress Features](#new-cypress-features)
- [Useful Resources](#useful-resources)

## What is UI Testing?

UI (User Interface) testing involves testing the graphical interface of an application to ensure that it behaves as expected. This includes checking how elements like buttons, forms, and text fields respond to user actions. UI testing is an important part of maintaining quality in software, as it ensures users can interact with the application seamlessly.

### UI Testing vs. E2E Testing

UI testing focuses specifically on the frontend (how a user interacts with the application), while **End-to-End (E2E)** testing tests the entire flow of an application—from the frontend to the backend, database, and external systems.

| Feature              | UI Testing                              | End-to-End Testing                     |
|----------------------|------------------------------------------|----------------------------------------|
| **Focus**            | Testing user interface and interactions | Testing the full user journey          |
| **Components Tested**| Frontend only                           | Frontend, backend, database, APIs      |
| **Tools**            | Cypress, Selenium, Puppeteer            | Cypress, Playwright                    |
| **Use Cases**        | Testing individual elements or flows    | Ensuring the entire app works as a whole|

### Example Scenarios

Here are some scenarios where UI testing is typically used:

- **Login form** – verifying that the form behaves as expected when correct or incorrect credentials are entered.
- **Search feature** – checking that entering a search term returns the correct results.
- **Form submission** – ensuring that forms validate user input and provide appropriate success or error messages.

## Using Cypress for UI Testing

Cypress is a popular framework for writing automated tests for web applications. It is particularly good at UI and E2E testing due to its ability to interact directly with the browser in real-time.

### Setting Up Cypress

To get started with Cypress, follow these steps:

1. **Create a New Project**

   First, create a new directory for your project:

   ```bash
   mkdir cypress-tutorial
   cd cypress-tutorial
   ```

2. **Initialize the Project**
   Initialize the project and install Cypress by running:

    ```bash
    npm init -y
    npm install cypress --save-dev
    ```

3. **Open Cypress**
   Once installed, you can open Cypress using the following command:
    ```bash
    npx cypress open
    ```
   Cypress will open a test runner window, where you can create and run tests.

### Common Commands

Here are some common commands you'll use frequently when writing UI tests in Cypress:

| Command               | Description                                                 |
|-----------------------|-------------------------------------------------------------|
| `cy.visit(url)`        | Visits a specific URL                                       |
| `cy.get(selector)`     | Grabs an element based on a CSS selector                    |
| `cy.contains(text)`    | Finds an element that contains the specified text           |
| `cy.click()`           | Clicks on an element                                        |
| `cy.type(text)`        | Types into an input field                                   |
| `cy.should(condition)` | Asserts that an element meets a certain condition           |
| `Cypress.stop()`       | Stops the Cypress test run when called; helpful to exit early when conditions aren't met. |
| `cy.press(key)`        | Dispatches native keyboard events such as Tab to test focus and keyboard navigation. |
| `cy.intercept(url, options)` | Intercepts HTTP requests and responses, enabling you to stub or spy on network calls. |

## Example Scenarios and Tests
Here are a few scenarios that show how Cypress can be used for UI testing:

### UI Testing Scenarios:

#### Scenario 1: Testing a Login Form
This test checks if the login form functions as expected when correct and incorrect credentials are submitted.

```typescript
describe('Login Form', () => {
  it('Should show error for incorrect credentials', () => {
    cy.visit('/login');
    cy.get('input[name="email"]').type('wrong@example.com');
    cy.get('input[name="password"]').type('wrongpassword');
    cy.get('button[type="submit"]').click();
    cy.contains('Invalid credentials').should('be.visible');
  });

  it('Should successfully login with correct credentials', () => {
    cy.visit('/login');
    cy.get('input[name="email"]').type('user@example.com');
    cy.get('input[name="password"]').type('correctpassword');
    cy.get('button[type="submit"]').click();
    cy.url().should('include', '/dashboard');
  });
});
```

#### Scenario 2: Testing a Search Feature
This test verifies that searching for a keyword returns the correct results.
```typescript
describe('Search Feature', () => {
  it('Should display search results when a keyword is entered', () => {
    cy.visit('/search');
    cy.get('input[name="search"]').type('Cypress');
    cy.get('button[type="submit"]').click();
    cy.contains('Search Results for Cypress').should('be.visible');
    cy.get('.result-item').should('have.length.greaterThan', 0);
  });
});
```

#### Scenario 3: Form Submission and Validation
In this scenario, we check if a form validates input and submits correctly.

```typescript
describe('Form Submission', () => {
  it('Should display validation errors for empty fields', () => {
    cy.visit('/form');
    cy.get('button[type="submit"]').click();
    cy.contains('This field is required').should('be.visible');
  });

  it('Should submit the form when all fields are filled', () => {
    cy.visit('/form');
    cy.get('input[name="name"]').type('John Doe');
    cy.get('input[name="email"]').type('john@example.com');
    cy.get('input[name="phone"]').type('1234567890');
    cy.get('button[type="submit"]').click();
    cy.contains('Form submitted successfully').should('be.visible');
  });
});
```

### E2E Testing Scenarios:
E2E tests are typically used to validate the entire flow of an application, including frontend, backend, and external systems.

## Where to Place Cypress Tests
Here is the typical structure of a modern Cypress project (Cypress 10 and later). In version 10 the old `cypress/integration` folder was renamed to `cypress/e2e` and spec files now end with `.cy.[ext]`. The support file and configuration file have also been renamed.

### 1. Cypress Folder Structure:

After running `npx cypress open`, Cypress will scaffold a directory structure similar to the following:

```bash
cypress/
├── e2e/          # Test files (formerly the `integration` folder)
├── fixtures/     # Test data (JSON files) for mocking server responses
├── support/
│   ├── e2e.js    # Support file for E2E tests (renamed from `support/index.js`)
│   └── component.js  # Support file for component testing (if you enable component tests)
└── cypress.config.js  # New configuration file replacing `cypress.json`
```

### 2. Create Test Files:

Inside the `cypress/e2e` directory, create separate test files for each feature you want to test. With Cypress 10 and above, the recommended file extensions end in `.cy.ts` or `.cy.js`:

```bash
cypress/
├── e2e/
│   ├── login.cy.ts           # Login tests
│   ├── search.cy.ts          # Search tests
│   ├── formSubmission.cy.ts  # Form submission tests
```

### 3. Adding `describe` Blocks:

Each test file should contain one or more `describe` blocks that group related tests. These blocks and individual `it` blocks go inside the respective test files. For example:

```typescript
// cypress/e2e/login.cy.ts
describe('Login Form', () => {
  // individual tests inside `it` blocks
});
```

### 4. Running Tests:

You can run all tests either through the Cypress Test Runner or in headless mode with:

```bash
npx cypress run
```

### 5. Component Testing (Optional):

Cypress 10 introduced first‑class component testing support. To enable component tests, Cypress will scaffold additional files (for example, `cypress/support/component.js` and `component-index.html`) after you choose a framework during setup. Component tests live alongside your E2E tests but focus on testing individual UI components in isolation.

## New Cypress Features

Recent releases of Cypress (versions 14 and later) introduced several powerful capabilities to improve test stability and flexibility. The following features are particularly useful when writing UI and end‑to‑end tests:

- **`Cypress.stop()`** – Stops the Cypress test run immediately when invoked. For example, you can add an `afterEach` hook to stop the run if a test fails:
  ```typescript
  afterEach(function () {
    if (this.currentTest.state === 'failed') {
      Cypress.stop();
    }
  });
  ```

- **`cy.press(key)`** – Dispatches native keyboard events such as the Tab key to test focus management and keyboard navigation. This helps test accessibility features and keyboard interactions:
  ```typescript
  cy.get('input.first').focus();
  cy.press(Cypress.Keyboard.Keys.TAB);
  cy.get('input.second').should('have.focus');
  ```

- **`cy.intercept(url, options)`** – Intercepts and optionally modifies HTTP requests and responses during a test. This command is useful for simulating different server responses or network conditions without changing your backend:
  ```typescript
  // Intercept requests to /api/data and return a mock response
  cy.intercept('/api/data', {
    statusCode: 200,
    body: { data: 'Test Data' },
  });
  ```

These new commands allow you to control test execution, simulate real keyboard interactions, and stub or spy on network requests to build more resilient and comprehensive test suites:

## Useful Resources

- [Cypress Official Documentation](https://docs.cypress.io)
- [Cypress Best Practices](https://docs.cypress.io/guides/references/best-practices)
- [End-to-End Testing with Cypress](https://docs.cypress.io/guides/core-concepts/introduction-to-cypress)
