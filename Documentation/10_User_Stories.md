# 10. Agile User Stories: User Profile Setup Module

## Overview
These granular user stories map out the functional scope for Phase 1 MVP (Sprint 1), translating the high-level business goals found in the BRD directly into actionable engineering backlog items.

---

### US-01: Mobile Registration via SMS OTP
**As a** new app user (Requestor or Volunteer),  
**I want to** register utilizing my mobile phone number and a 6-digit verification code,  
**So that** I can establish a secure, verified account on the platform without setting a complex password.

**Acceptance Criteria (AC):**
* [ ] **AC-01:** The registration interface must restrict input to numeric values exactly matching regional 10-digit formats.
* [ ] **AC-02:** Upon clicking "Send Code", the system must trigger a secure call to the integrated SMS Gateway API (Twilio) to dispatch a 6-digit random token.
* [ ] **AC-03:** The application must display a real-time countdown timer initialized at 05:00 minutes. The token must automatically expire when this timer reaches zero.
* [ ] **AC-04:** If an incorrect or expired code is submitted, the system must block progression and display an alert: `"Invalid or expired verification code. Please request a new token."`

---

### US-02: Capture Core Profile Details
**As a** newly authenticated user,  
**I want to** input my first name, last name, a brief bio, and select my help capabilities,  
**So that** other participants in the local network can recognize my profile and understand my skills.

**Acceptance Criteria (AC):**
* [ ] **AC-01:** The profile setup page must require fields for `First Name` and `Last Name` with a 50-character limit each.
* [ ] **AC-02:** The `About Me / Bio` field must be an optional text box with a strict character ceiling enforced at 300 characters.
* [ ] **AC-03:** The interface must present a multi-select component populated with at least 5 predefined capability tags (e.g., Grocery Shopping, Dog Walking, Pharmacy Pickup).
* [ ] **AC-04:** The system must implement an auto-save capability that triggers if the application enters a background execution state before form submission.

---

### US-03: Asynchronous Identity Verification (IDV)
**As a** registered Volunteer,  
**I want to** take a photo of my government-issued identification document within the app,  
**So that** my document can be routed for background verification to unlock user matching permissions.

**Acceptance Criteria (AC):**
* [ ] **AC-01:** The application front-end must check file input parameters and reject any image payload exceeding a maximum boundary of 5MB.
* [ ] **AC-02:** Upon image submission, the system must execute an asynchronous POST request to transmit the binary file data securely to the Stripe Identity API gateway.
* [ ] **AC-03:** While waiting for the API callback payload, the user record state in the database must be flagged as `status = verification_pending`.
* [ ] **AC-04:** The application interface must dynamically display a locked dashboard message to the user: `"Your identity document is currently undergoing verification. Account actions are restricted."`
