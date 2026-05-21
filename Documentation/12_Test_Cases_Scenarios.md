# 13. Test Cases & Test Scenarios: Onboarding Module

## Purpose
This document outlines the functional test scenarios and explicit test cases used by the Quality Assurance (QA) team to verify the compliance of the User Onboarding and Identity Verification module. These cases guarantee coverage for **US-01**, **US-02**, and **US-03**.

---

## 1. Test Scenario 1: Mobile Registration & OTP Validation (US-01)

### Test Case ID: TC-ONB-01 (Happy Path - Successful Registration)
* **Pre-conditions:** User has a valid, unregistered 10-digit mobile number.
* **Test Steps:**
  1. Open the app and select account type "Volunteer".
  2. Enter a valid 10-digit mobile number and click "Send Code".
  3. Retrieve the 6-digit OTP code sent via the Twilio simulator.
  4. Enter the correct 6-digit OTP code into the input fields and click "Verify & Submit".
* **Expected Result:** Token is validated successfully against `D1: Security/Token Log`, and the user is redirected to the "Profile Setup" screen.

### Test Case ID: TC-ONB-02 (Negative Path - Expired OTP Token)
* **Pre-conditions:** An OTP token has been generated but has exceeded the 5-minute lifecycle constraint (`NFR-SEC-03`).
* **Test Steps:**
  1. Complete steps 1-2 of TC-ONB-01.
  2. Wait exactly 5 minutes and 10 seconds.
  3. Enter the received 6-digit OTP code and click "Verify & Submit".
* **Expected Result:** The system rejects the entry, blocks navigation, and displays an explicit error alert: `"Invalid or expired verification code. Please request a new token."`

---

## 2. Test Scenario 2: Profile Detail Ingestion (US-02)

### Test Case ID: TC-ONB-03 (Boundary Path - Character Constraints)
* **Pre-conditions:** User has successfully verified their mobile number.
* **Test Steps:**
  1. On the Profile Setup screen, attempt to type a First Name exceeding 50 characters.
  2. Paste a text string of 350 characters into the "About Me / Bio" field.
* **Expected Result:** The UI input fields truncate text strictly at the 50-character limit for the name and the 300-character ceiling for the bio. The user cannot input characters past these boundaries.

---

## 3. Test Scenario 3: Asynchronous Identity Verification (US-03)

### Test Case ID: TC-ONB-04 (Exception Path - Payload Size Restriction)
* **Pre-conditions:** User is on the ID upload screen.
* **Test Steps:**
  1. Click the "Upload Government ID" target area.
  2. Select an image file (`.png`) that has a file size of 6.2MB.
* **Expected Result:** The client-side application rejects the file instantly before transmission and triggers a modal error: `"Unsupported file type or size exceeds 5MB."`

### Test Case ID: TC-ONB-05 (Happy Path - Async Webhook Execution)
* **Pre-conditions:** User uploads a valid 2MB `.jpg` image of a driver's license.
* **Test Steps:**
  1. Upload the valid ID image and click "Initialize Account".
  2. Check the database state for the user record in `D2: User Registry Profile Database`.
  3. Simulate a successful asynchronous verification callback payload from the Stripe Identity API.
  4. Check the updated database state for the user record.
* **Expected Result:** Upon submission, the database user flag instantly reads `status = verification_pending`. Following the API callback execution, the flag updates automatically to `status = vetted_volunteer`.
