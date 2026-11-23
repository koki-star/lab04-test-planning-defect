# Lab: Test Planning and Defect Management

## Topics

- Test planning
- Test case design
- Test execution
- Defect reporting
- Confirmation testing

## Learning Objectives

- Create a test plan for a small application.
- Define test objectives, scope, risks, and entry and exit criteria.
- Design and execute test cases.
- Compare expected and actual results.
- Write a reproducible defect report.

# Deliverables

## Step 1: Create a Test Plan

This is my brief test plan for the Counter application.

### Test objectives

- Check that the count starts at 0 when the app opens.
- Check that Increment adds 1 to the count.
- Check that Decrement subtracts 1 from the count.
- Check that Reset sets the count back to 0.
- Check that the buttons still work after a sequence of clicks.

### What is in and out of scope

In scope:
- The starting count
- The Increment, Decrement, and Reset buttons
- The count value shown on the page after each click

Out of scope:
- How the page looks (colors, layout, and style)
- Running the app on a phone
- Saving the count after I close the app

### The testing approach

I will write the test cases first. Then I will run them with Jest and React Testing Library (tools that render the app and click the buttons for me). I will compare the expected result to the actual result for each test. If a test fails, I will run it again. That is confirmation testing (checking that the same problem happens a second time).

### The test environment and tools

- Computer: MacBook Pro (M1), macOS
- Browser: Chrome
- Tools: Node.js, Jest, and React Testing Library
- Editor: VS Code

### Product risk

One product risk (a problem in the app that could hurt the user) is that the Decrement button might not lower the count. If that happens, the user cannot count down, and the button label would be wrong.

### Entry and exit criteria

Entry criteria (what must be true before testing starts):
- The app starts with `npm run dev` and shows the count and the three buttons.
- The test cases are written.
- Jest is installed and `npm test` runs.

Exit criteria (what must be true before testing is done):
- All planned test cases are run.
- Any failed test is run a second time.
- A defect report is written for any defect that was found, or a short note is written if no defect was found.

## Step 2: Design Test Cases

I wrote five test cases. TC4 and TC5 use more than one action in a sequence.

| Test Case ID | Starting State | Actions | Expected Result |
| --- | --- | --- | --- |
| TC1 | The app just opened. The count is 0. | Look at the page. | The page shows Count: 0. The Increment, Decrement, and Reset buttons are on the page. |
| TC2 | The count is 0. | Click Increment once. | The page shows Count: 1. |
| TC3 | The count is 0. | Click Decrement once. | The page shows Count: -1. |
| TC4 | The count is 0. | Click Increment twice. Then click Reset once. | After two Increment clicks, the page shows Count: 2. After Reset, the page shows Count: 0. |
| TC5 | The count is 0. | Click Increment three times. Click Decrement once. Click Reset once. Click Decrement once. | After three Increment clicks, the page shows Count: 3. After Decrement, the page shows Count: 2. After Reset, the page shows Count: 0. After the last Decrement, the page shows Count: -1. |

## Step 3: Execute the Tests

I ran the tests with `npm test` in the `counter-app` folder. The first run showed this summary:

```text
Test Suites: 1 failed, 1 total
Tests:       2 failed, 3 passed, 5 total
```

TC3 and TC5 failed, so I ran `npm test` a second time. The second run showed the same summary:

```text
Test Suites: 1 failed, 1 total
Tests:       2 failed, 3 passed, 5 total
```

The same two tests failed again with the same actual results, so the defect can be reproduced.

| Test Case ID | Actual Result | Pass or Fail |
| --- | --- | --- |
| TC1 | The page showed Count: 0 and all three buttons. | Pass |
| TC2 | The page showed Count: 1. | Pass |
| TC3 | The page showed Count: 1, not Count: -1. | Fail |
| TC4 | After two Increment clicks the page showed Count: 2. After Reset it showed Count: 0. | Pass |
| TC5 | After three Increment clicks the page showed Count: 3. After Decrement it showed Count: 4, not Count: 2. The test stopped at that step. | Fail |

## Step 4: Report a Defect

### Defect ID and title

DEF-001: Decrement button increases the count instead of decreasing it

### Related test case

TC3 and TC5

### Test environment

MacBook Pro (M1), macOS, Node.js, Chrome, Jest and React Testing Library

### Steps to reproduce

1. Open the Counter app, or run `npm test`.
2. Confirm the count starts at 0.
3. Click the Decrement button once.

### Expected result

The page shows Count: -1.

### Actual result

The page shows Count: 1. The count went up by 1, the same as Increment. In TC5, after the count was 3, one Decrement click changed it to 4.

### Severity and priority

Severity (how bad the problem is for the user): High. Decrement is a main button, and it does the opposite of what the label says. The user cannot lower the count at all.

Priority (how soon it should be fixed): High. This should be fixed first because a core action is broken.

### Status

Open

## How to Run

Go to the `counter-app` folder, then use these commands in the VS Code terminal.

```bash
cd counter-app
```

This moves you into the app folder.

```bash
npm install
```

This installs the packages the app and the tests need.

```bash
npm test
```

This runs the Jest tests and shows pass or fail for each test case.

```bash
npm run dev
```

This starts the app in the browser so you can click the buttons yourself.

## AI Transparency

AI was used to create part of this file and to clean up its writing and formatting.
