# 15. Formally Managed Change Request (CR) & Impact Analysis

## 1. Change Request Overview
* **Change Request ID:** CR-2026-004
* **Project Name:** HelpLocal MVP (Onboarding & Security Framework)
* **Date Requested:** May 21, 2026
* **Requested By:** Elena Rostova (VP of Community Operations)
* **Assigned Analyst:** Naveen Shanmugam (Senior BA)
* **Status:** Evaluated / Awaiting Steering Committee Disposition

---

## 2. Description of Requested Modification
The business sponsor requests an immediate mid-sprint modification to accelerate a deferred Phase 2 feature into the Phase 1 MVP launch scope. 

* **The Request:** Implement a real-time, automated geofencing calculation during user registration. The application must capture the volunteer's latitude and longitude and restrict assignment visibility strictly to a 5-kilometer localized operational radius.
* **Original Scope Alignment:** Per section 3.2 of the **BRD (Step 5)**, radius lookup automation was explicitly flagged as *Out-of-Scope* for the initial release, with manual area codes serving as the baseline data point.

---

## 3. Comprehensive Impact Analysis

### A. Core Documentation & Traceability Impact
* **Requirements Traceability Matrix (RTM Step 4):** Requires the injection of two brand-new functional lines: `FR-CORE-GEO-01` (GPS Ingestion) and `FR-CORE-GEO-02` (Radius Filtering Logic).
* **Data Dictionary (Step 9):** The `User Registry Profile Database` schema must be altered to accommodate two new technical data fields: `latitude` (Decimal 9,6) and `longitude` (Decimal 9,6). Both elements must be flagged as mandatory inputs.

### B. Engineering & Process Flow Impact
* **BPMN Process Flow (Step 7):** Modifies the Front-End and Back-End lane interactions. A mobile device location prompt block must be added immediately following successful OTP verification.
* **Architectural Blockers:** Introducing mobile location runtime permission handshakes increases the probability of user onboarding drop-offs if permission is denied. An exception sub-flow must be architected to handle fallback inputs gracefully.

### C. Schedule, Timeline & Testing Volumetrics
* **Development Estimate:** 4 Additional Developer Days required to integrate device-level location APIs and configure query indexing profiles on the database layer.
* **Quality Assurance Impact:** Requires 3 additional Test Cases to evaluate edge scenarios (e.g., GPS spoofing, device location services disabled, and boundary conditions at exactly 5.01 kilometers).
* **Target Release Impact:** Pushing this modification into Sprint 3 will delay the production deployment timeline by precisely **1 calendar week**.

---

## 4. Business Recommendation & Trade-Offs
As Lead Business Analyst, my formal recommendation is to **reject immediate implementation within Phase 1 MVP** and stick to the original product roadmap. 

* **Alternative Resolution:** Keep the database field modifications within the upcoming deployment to ensure data compatibility, but disable the automated front-end lookup rules until Sprint 4 begins. This mitigates launch slippage risks while allowing engineering teams to lay structural foundations early.
