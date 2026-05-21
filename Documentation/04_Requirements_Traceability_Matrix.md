# 04. Requirements Traceability Matrix (RTM): Project HelpLocal

## Purpose
This matrix ensures strict alignment between high-level business drivers and technical execution. It tracks requirements throughout the software development lifecycle (SDLC), ensuring that verification and testing criteria are met before deployment.

| Business Req ID | Business Goal / Objective | Functional Req ID | Software Feature Description | Agile User Story ID | Test Case ID | Sprint Alignment | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **BR-01** | Establish community trust and safety parameters. | **FR-01** | System must integrate with a 3rd party IDV API (e.g., Stripe Identity) to verify volunteer documents. | `US.03` | `TC-03` | Sprint 1 | In Progress |
| **BR-01** | Establish community trust and safety parameters. | **FR-02** | System must prevent unverified accounts from viewing requestor addresses. | `US.02` | `TC-02` | Sprint 1 | In Progress |
| **BR-02** | Enable rapid, frictionless user onboarding. | **FR-03** | System must support mobile registration utilizing a 6-digit SMS One-Time Password (OTP). | `US.01` | `TC-01` | Sprint 1 | Complete |
| **BR-03** | Optimize localization and matching logic. | **FR-04** | System must allow users to multi-select predefined help capability tags during setup. | `US.04` | `TC-04` | Sprint 1 | Complete |

## Matrix Legend & Key
* **BR:** Business Requirement (Derived from the Business Case)
* **FR:** Functional Requirement (System behavior defined in the BRD)
* **US:** User Story ID (Tracked within the Jira Product Backlog)
* **TC:** Test Case ID (Utilized by QA for User Acceptance Testing)
