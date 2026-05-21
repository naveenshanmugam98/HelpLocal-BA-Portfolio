# 05. Business Requirements Document (BRD): Project HelpLocal

## 1. Document Control
* **Project Name:** HelpLocal MVP (Onboarding & Security Framework)
* **Version:** 1.0
* **Author:** Naveen Shanmugam (Senior Business Analyst)
* **Status:** Draft / Ready for Review

---

## 2. Introduction & Business Objectives
The purpose of this document is to formalize the business and functional software requirements for the initial Minimum Viable Product (MVP) of HelpLocal. 

The primary business drivers are:
* **Objective 1:** Establish a trusted ecosystem by ensuring 100% identity verification for high-influence users (Volunteers).
* **Objective 2:** Ensure digital accessibility compliance for vulnerable demographics (Seniors) to encourage adoption.
* **Objective 3:** Mitigate operational liability by restricting system data visibility based on user verification states.

---

## 3. Project Scope
Managing scope boundaries is critical to maintaining a predictable sprint cadence and avoiding development blockages.

### 3.1 In-Scope (Phase 1 MVP - Sprints 1-3)
* Dual-persona account initialization framework (Requestor vs. Volunteer profiles).
* Integration with a third-party Identity Verification (IDV) web hook service.
* Multi-factor verification via SMS One-Time Password (OTP) processing.
* Core profile configuration capabilities (adding profile image, bio text, and help capability tags).

### 3.2 Out-of-Scope (Deferred to Phase 2+)
* In-app automated payment processing, digital wallet integrations, and tipping mechanics.
* Comprehensive background check integration via national criminal or law enforcement registries.
* Geofencing-driven automated push notifications (initial iteration will utilize standard radius lookup queries).

---

## 4. Detailed Functional Requirements
These high-level software requirements define the system behavior needed to fulfill the project's strategic objectives.

### 4.1 Account Authentication & Security
* **FR-01:** The system must accept a valid 10-digit mobile number and send a 6-digit alphanumeric One-Time Password (OTP) via an SMS gateway API (e.g., Twilio).
* **FR-02:** The system must invalidate the generated OTP precisely 5 minutes after initiation to prevent brute-force attacks.

### 4.2 Profile Management & Verification
* **FR-03:** The user interface must support image file ingestion (`.jpg`, `.jpeg`, `.png`) restricted to a maximum size threshold of 5MB for profile imagery.
* **FR-04:** For Volunteer profiles, the software must route uploaded identity documentation directly to the integrated IDV API vendor and await an asynchronous confirmation payload.
* **FR-05:** The system must structurally restrict the visibility of the primary Requestor's physical address records; it must remain hidden until a Vetted Volunteer explicitly accepts an associated assignment.

---

## 5. Assumptions & Constraints
* **Assumption A:** End-users utilize smartphones running modern mobile operating systems (iOS 15+ or Android 11+) equipped with functional front-facing cameras for document scanning.
* **Constraint B:** The storage and processing architecture of user identity payloads must comply entirely with regional data confidentiality guidelines and data residency mandates.
