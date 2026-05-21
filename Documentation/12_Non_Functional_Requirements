# 12. Non-Functional Requirements (NFR) Document

## Purpose
This document establishes the structural quality attributes, performance thresholds, and security compliance parameters for the HelpLocal MVP onboarding module. These specifications serve as the baseline criteria for engineering architecture and QA system testing.

---

## 1. Security, Privacy & Data Integrity
* **NFR-SEC-01 (Data Encryption):** All personally identifiable information (PII)—including mobile numbers, bio text fields, and government ID image binaries—must be encrypted at rest using AES-256 and in transit using TLS 1.3.
* **NFR-SEC-02 (API Authentication):** All communication boundaries with external microservices (Twilio SMS Gateway and Stripe Identity API) must be authorized via secure HTTPS protocols using signed OAuth 2.0 bearer tokens.
* **NFR-SEC-03 (Data Purging):** To mitigate data liability, transient verification tokens (`otp_token`) must automatically purge from active cache memory precisely 5 minutes post-generation.

---

## 2. Performance, Latency & Scalability
* **NFR-PER-01 (API Response Latency):** The backend authentication engine must validate phone string formats, generate the random token, and pass the payload to the Twilio gateway within a round-trip constraint of <200ms under baseline loads.
* **NFR-PER-02 (Concurrent User Volumetrics):** The application infrastructure must scale to comfortably support up to 5,000 concurrent active sessions during peak operational hours without causing system degradation.
* **NFR-PER-03 (UI Thread Ingestion):** Ingestion pipelines handling the maximum 5MB `id_image_binary` payload must run asynchronously, ensuring that client-side front-end rendering does not freeze or lock up during transmission.

---

## 3. Reliability, Availability & Fault Tolerance
* **NFR-REL-01 (Core System Uptime):** The identity verification and database cluster microservices must maintain an active availability threshold of 99.9% uptime (calculated monthly, excluding pre-scheduled infrastructure maintenance windows).
* **NFR-REL-02 (Graceful Error Handling):** If an external service dependency encounters a critical outage (e.g., Twilio cellular networks drop), the application must fail gracefully by capturing the network timeout and rendering a localized UI error: `"Authentication networks are currently congested. Please retry in 2 minutes."` instead of terminating the system process.
