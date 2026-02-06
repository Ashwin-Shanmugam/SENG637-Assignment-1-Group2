# Lab Report

## High-Level Description of the Exploratory Testing Plan

### Test Specifications
Testing will be timed to 30 minutes to allow for rapid familiarization without getting bogged down in documentation.

One team member will operate the SUT, interacting with the GUI.

The second team member will guide the testing, observe results, and immediately log any defects found into the defect tracking system to ensure detailed conditions are not forgotten.

We will use the ATM System - Lab 1 Version 1.0.jar with the provided valid data: Card #1 and Card #2.

### Scope of Testing
The scope of this session is the System Under Test GUI simulation. We will target the following high-level functions based on the system requirements:

- System Startup/Shutdown: Powering on/off and entering initial cash on hand.
- Session Management: Valid login, invalid login, and card retention after 3 failed attempts.
- Financial Transactions:
- Withdrawal: Verifying denominations ($20 multiples) and insufficient fund handling.
- Deposit: Verifying envelope insertion simulation and amount entry.
- Transfer: Moving funds between Checking and Savings.
- Balance Inquiry: Viewing current balances.
- Cancellation: Aborting transactions at various stages (e.g., before inserting envelope or selecting amount).

### Testing Approach and Strategy
We will utilize a Hybrid Approach combining "Breadth-First" testing with "Exceptional Path" testing.

Breadth-First Strategy (First 15 minutes):
Goal: Touch every main menu function (Withdraw, Deposit, Transfer, Inquiry) at least once.
Method: We will execute scenarios using valid inputs (e.g., withdraw $20 from Card 1 Checking) to verify the system performs its core purpose: allowing the user to perform transactions successfully.
Target: Ensure the specific expected outcomes (e.g., receipt printing, balance updates) occur as defined in the requirements.

Exceptional Path Strategy (Last 15 minutes):
- Goal: Break the system by testing edge cases and invalid inputs.
- Method: We will deviate from standard use to test error handling.
- Scenario A: Enter 0 or negative numbers for initial cash on hand.
- Scenario B: Attempt to withdraw more money than is in the account, or an amount not divisible by $20.
- Scenario C: Enter an incorrect PIN three times to verify card retention.
- Scenario D: Press "Cancel" immediately after selecting a transaction type.

### Justification of Plan
This plan is chosen because the primary objective of this phase is familiarization. By starting with a breadth-first approach, we ensure we understand the baseline behavior of the SUT. Switching to exceptional path testing in the second half allows us to identify robustness issues and potential crashes early, which maximizes the value of the unscripted nature of exploratory testing. This covers both the normal operation and error scenarios required to gauge system stability.
