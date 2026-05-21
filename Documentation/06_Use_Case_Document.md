# 06. Use Case Document: User Account Onboarding & Verification

## Use Case ID: UC-01
**Use Case Name:** Register Account and Verify Volunteer Identity  
**Primary Actor:** New Volunteer  
**Secondary Actors:** SMS Gateway API (Twilio), Identity Verification (IDV) API, Core Database  

---

## 1. Pre-conditions
1. The user has downloaded and opened the HelpLocal application.
2. The user has a functional smartphone with an active network connection capable of receiving SMS messages and a camera for scanning documents.

## 2. Post-conditions
* **Success End State:** The user's account is initialized, identity documents are routed to the IDV vendor, and the account status is updated to "Verification Pending" in the Core Database.
* **Failure End State:** The system logs the failure, displays an error message to the user, and restricts access to core application workflows.

---

## 3. Main Success Scenario (The "Happy Path")
1. The User selects the "Register as Volunteer" option on the app splash screen.
2. The User enters their mobile phone number and clicks "Send Code".
3. The System triggers a call to the **SMS Gateway API** to dispatch a 6-digit One-Time Password (OTP).
4. The User receives and enters the 6-digit OTP into the app interface.
5. The System validates the OTP and displays the "Identity Setup" screen.
6. The User fills out their profile details (Name, Bio, Capability Tags) and uploads a clear photo of their Government ID.
7. The System securely transmits the ID image payload to the **IDV API vendor** via an asynchronous webhook call.
8. The System records the user record in the **Core Database** with a flag setting of `status = verification_pending`.
9. The System displays a confirmation screen stating: "Your identity verification is being processed."

---

## 4. Alternative Flows
### Alternative Flow 3A: Incorrect OTP Input
* **3A.1:** At step 4 of the main flow, the user enters an invalid 6-digit code.
* **3A.2:** The system displays an error message: "Invalid code. Please try again." and resets the input field.
* **3A.3:** The flow returns to Step 4 of the main success scenario.

### Alternative Flow 3B: OTP Code Timeout
* **3B.1:** The user fails to enter the OTP code within 5 minutes of transmission.
* **3B.2:** The system invalidates the token, displays an error message: "Session expired," and shows a "Resend Code" link.
* **3B.3:** The user clicks "Resend Code," and the loop resets to Step 3 of the main success scenario.

---

## 5. Exception Flows
### Exception Flow 6A: Invalid Image Upload Format or Size
* **6A.1:** At step 6 of the main flow, the user attempts to upload a file exceeding 5MB or using an unsupported format (e.g., `.gif`).
* **6A.2:** The system rejects the file ingest block and displays a real-time error alert: "Unsupported file type or size exceeds 5MB."
* **6A.3:** The user is prevented from advancing until a valid image file (`.jpg`, `.png`) is provided.
