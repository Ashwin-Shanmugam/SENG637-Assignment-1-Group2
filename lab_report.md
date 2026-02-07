**SENG 637 - Dependability and Reliability of Software Systems**
>   **Assignment \#1**
>   **Introduction to Testing and Defect (Bug) Tracking**  
>   Instructor: Dr. Behrouz Far (far@ucalgary.ca)
>   Department of Electrical and Software Engineering
>   University of Calgary

Due Date: Check D2L for the submission deadline.

| Group: 2 |
|---|
| Ashwin |
| Salehin |
| Noshin |
| Jasneet |

**Table of Contents**

(When you finish writing, update the following list using right click, then “Update Field”)

[1 Introduction	1](#introduction)  
[2 High-level description of the exploratory testing plan	1](#high-level-description-of-the-exploratory-testing-plan)  
[3 Comparison of exploratory and manual functional testing	1](#comparison-of-exploratory-and-manual-functional-testing)  
[4 Notes and discussion of the peer reviews of defect reports	1](#notes-and-discussion-of-the-peer-reviews-of-defect-reports)  
[5 How the pair testing was managed and team work/effort was divided	1](#how-the-pair-testing-was-managed-and-team-workeffort-was-divided)  
[6 Difficulties encountered, challenges overcome, and lessons learned	1](#difficulties-encountered-challenges-overcome-and-lessons-learned)  
[7 Comments/feedback on the lab and lab document itself	1](#commentsfeedback-on-the-lab-and-lab-document-itself)  

# Introduction

The objective of this assignment was to gain practical experience with software testing techniques and defect tracking by testing an ATM system simulator. Across the lab activities, we applied:
- exploratory testing to quickly learn the system and discover unexpected behaviors,
- manual functional (scripted) testing to validate behavior against predefined test cases (Appendix C),
- regression testing to confirm that areas surrounding defects still behaved correctly after issues were identified.

Before completing this lab, our understanding of exploratory and manual functional testing was primarily conceptual. We understood exploratory testing as an adaptive process where test design and execution happen together, guided by observation and learning. We understood manual functional testing as executing predefined test cases step-by-step to validate expected behavior and maintain traceability to requirements. Performing both styles on the ATM simulator clarified how each approach finds different classes of defects, and how defect tracking quality determines whether findings are useful to developers and graders.

# High-level description of the exploratory testing plan

## Test specifications

- **Time boxing:** The exploratory session was limited to **30 minutes** to promote rapid familiarization and focused defect discovery.
- **Pair execution:** One team member operated the SUT through the GUI while the second member guided scenario selection, observed outcomes, and logged defects immediately in the defect tracking system.
- **Test environment:** Testing was performed on the **ATM System - Lab 1 Version 1.0.jar** using the provided valid test data (**Card #1 and Card #2**).

## Scope of exploratory testing

Exploratory testing targeted the simulator GUI and the major user-facing behaviors described in the requirements:
- **System startup/shutdown:** power on/off and entering initial cash on hand.
- **Session management:** valid login, invalid login, PIN retry handling, and card retention after three failed attempts.
- **Transactions:** withdrawal, deposit, transfer, and inquiry.
- **Cancellation behavior:** aborting transactions at different stages (for example, after choosing a transaction type, after entering an amount, and before inserting the envelope during deposits).

Out of scope for this assignment were non-functional concerns such as performance, stress testing, hardware failures, and network or communication failures.

## Testing approach and strategy

We used a hybrid exploratory strategy combining breadth-first and exceptional path exploration:

1. **Breadth-first strategy (first ~15 minutes)**
   - Goal: touch every main function at least once (Withdraw, Deposit, Transfer, Inquiry).
   - Method: execute representative valid scenarios (for example, withdraw $20 from checking) to confirm baseline behavior such as successful completion messages and balance updates.

2. **Exceptional path strategy (last ~15 minutes)**
   - Goal: probe error handling, boundary conditions, and state transitions.
   - Method: intentionally try invalid or edge inputs and unusual user actions, including:
     - entering 0 or negative values for initial cash on hand,
     - attempting withdrawal amounts not divisible by $20,
     - attempting transactions exceeding the available balance,
     - entering an incorrect PIN three times to verify retention,
     - pressing Cancel immediately after selecting a transaction type and at later stages in the flow.

## Justification of the plan

The purpose of the exploratory phase was to quickly learn system behavior and identify defect candidates that would be missed by only running the predefined scripts. Breadth-first exploration rapidly established functional familiarity, and exceptional-path exploration targeted robustness and usability issues, especially around validation logic and cancellation semantics. Findings from this phase informed where we paid extra attention during scripted testing and regression checks.

## Exploratory testing

Exploratory testing was effective for:
- discovering unexpected behaviors and confusing system messaging,
- testing realistic user actions not explicitly scripted (for example, pressing Cancel at non-obvious points),
- quickly identifying boundary and validation concerns (invalid inputs, invalid card handling, insufficient balance messaging).

Its limitations are that coverage is not guaranteed and traceability to requirements is weaker unless notes are carefully structured during execution.

## Exploratory Testing Findings Summary

The exploratory testing resulted in identifying 9 defects in Version 1.0. Several defects affected financial correctness, including incorrect withdrawal amounts, incorrect balance updates after deposits, and inaccurate receipt information. Security-related defects were also observed, such as failure to permanently retain cards after repeated invalid PIN attempts and redundant PIN entry after recovering from invalid authentication attempts.

Overall, exploratory testing was effective in revealing validation, security, and transaction flow defects that would likely be missed through scripted testing alone.

## Manual functional (scripted) testing

Manual scripted testing was performed using Appendix C. This approach was effective for:
- systematic coverage of required behaviors,
- repeatability, since steps and expected results are predefined,
- easier identification of exact requirement mismatches.

In our execution, **35 test cases** were run, covering authentication and invalid input handling, withdrawals and cancellation scenarios, deposit flows (including envelope handling), transfers and edge cases, inquiry transactions, and PIN retry behavior. Most test cases passed; a small subset exposed defects related to validation logic, error messaging, and transaction cancellation behavior.

Its limitations are that it can miss defects in flows not represented in the scripted suite, and it may not reveal usability or edge-case issues unless those are explicitly encoded in test cases.

# Comparison of exploratory and manual functional testing

Exploratory testing and manual functional (scripted) testing produced different benefits during this assignment.

## How they complement each other

Exploratory testing helped identify where the system might behave unexpectedly and guided attention toward high-risk behaviors such as cancellation boundaries and input validation. Scripted testing then confirmed expected behavior systematically and made it easier to document deviations precisely against expected outcomes.

## Regression Testing Results and Observations

During regression testing, previously reported defects from both exploratory and manual script testing in version 1.0 were re-executed against ATM version 1.1. Each defect was reviewed to determine whether the issue was resolved or persisted. Defects confirmed as fixed were marked as RESOLVED, while those still reproducible were marked as IN-PROGRESS with a comment “Defect still exists in version 1.1”.

# Notes and discussion of the peer reviews of defect reports

All defects were logged in the defect tracking system with clear reproduction steps, expected results, and actual results. After logging, we conducted peer reviews to improve defect report quality and consistency. The review focused on:

- **Reproducibility:** Steps were checked to ensure another tester could reproduce the issue without additional context.
- **Correctness of expectations:** Expected behavior was verified against the assignment requirements and scripted test cases.
- **Clarity:** Reports were edited to avoid vague statements and to include the exact input values and the exact point in the flow where the issue occurred (especially important for cancellation-related defects).
- **De-duplication:** Similar defects were compared to avoid duplicate reporting.

During review, particular attention was paid to defects involving transaction flow state, where misinterpreting the correct stopping point can lead to incorrectly reported issues. Examples of defects that were reviewed and finalized include:
- acceptance of invalid card numbers,
- incorrect error message for insufficient account balance,
- deposit processing despite cancellation prior to envelope insertion.

# How the pair testing was managed and team work/effort was divided 

## Pair testing management

During exploratory testing, we used a driver and navigator model:
- **Driver:** interacted with the ATM GUI and executed scenarios.
- **Navigator/observer:** guided scenario selection, monitored outputs, and logged defects immediately to capture accurate steps and outcomes.

This reduced missed observations and improved defect documentation quality.

## Work division across testing types

To ensure coverage and built-in review, responsibilities were distributed:
- **Ashwin:** exploratory testing (system familiarization, unexpected behaviors, usability issues, boundary conditions).
- **Salehin:** manual scripted testing (executing Appendix C test cases and recording pass/fail outcomes).
- **Noshin:** regression testing (re-executing relevant flows and previously passed tests after defects were observed in related areas).
- **Jasneet:** cross-review of testing outputs and documentation (spot-checking execution results, improving defect write-ups, and supporting report quality).

In addition, all members reviewed the final set of defect reports for consistency and completeness.

# Difficulties encountered, challenges overcome, and lessons learned

A major challenge was interpreting cancellation behavior correctly, especially for deposits and transfers where the user can cancel at multiple points and where prompts can suggest different transaction states. This required careful alignment with the test case wording and close observation of whether balances and confirmations indicated a committed transaction.

Other difficulties included:
- tracking expected balances accurately across multiple transactions,
- distinguishing true defects from unspecified behavior or ambiguous messaging,
- ensuring defect reports included enough detail (exact inputs, sequence, and timing of Cancel) for reliable reproduction.

Key lessons learned:
- precise test execution matters because small differences in input values or timing can change system state,
- defect documentation quality is part of testing quality, since unreproducible defects are not actionable,
- exploratory testing and scripted testing are complementary, with exploration finding surprising behaviors and scripts providing systematic coverage and traceability,
- regression re-checking is essential when defects relate to shared logic (validation and transaction state handling).

# Comments/feedback on the lab and lab document itself

The lab provided practical experience applying multiple testing techniques and reinforced the importance of documenting defects clearly. The ATM simulator and structured scripted test cases were useful for learning how expected behavior is validated and how defects are communicated.