# 11. Low-Fidelity Wireframes & UI Schema

## Purpose
These structural low-fidelity wireframes map out the visual layout, screen real estate allocation, and functional component hierarchy for the Phase 1 MVP Onboarding module. This layout directly implements the interface constraints required by **US-01**, **US-02**, and **US-03**.

---

### Screen A: Mobile Registration UI (US-01)
*Purpose: Handles initial phone collection and account type assignment.*

| User Interface Component Layout | Component Metadata & Actions |
| :--- | :--- |
| <pre>📱 ---------------------------------- 📱<br>\|           HelpLocal MVP            \|<br>\|       [ Community Errand App ]     \|<br>\|                                    \|<br>\|  Enter your mobile number to begin \|<br>\|  registration. Secure SMS validation\|<br>\|  will execute immediately.         \|<br>\|                                    \|<br>\|  Mobile Number:                    \|<br>\|  [ +1 ] [ (555) 000-0000         ] \|<br>\|                                    \|<br>\|  Select Account Type:              \|<br>\|  ( ) Requestor (Need Chores Done)  \|<br>\|  (*) Volunteer (Want to Assist)    \|<br>\|                                    \|<br>\|       ======================       \|<br>\|       \|\|    SEND SMS CODE   \|\|       \|<br>\|       ======================       \|<br>📱 ---------------------------------- 📱</pre> | **1. Phone Input Field:**<br>• Type: Alphanumeric (Formatted String)<br>• Validation: Restrict to numeric input only.<br><br>**2. Account Type Selection:**<br>• Component: Radio Button Group<br>• Logic: Mutual exclusivity enforced. Default state is unselected.<br><br>**3. Primary Action Button:**<br>• Label: `SEND SMS CODE`<br>• Event: Triggers `FR-01` to invoke the Twilio API payload transfer. |

---

### Screen B: OTP Token Challenge UI (US-01)
*Purpose: Security validation workflow preventing unauthorized data manipulation.*

| User Interface Component Layout | Component Metadata & Actions |
| :--- | :--- |
| <pre>📱 ---------------------------------- 📱<br>\|        Account Verification        \|<br>\|                                    \|<br>\|  We have dispatched a 6-digit verification\|<br>\|  token via SMS to +1 (555) 000-0000\|<br>\|                                    \|<br>\|  Enter Validation Token:           \|<br>\|  [ 4 ] [ 9 ] [ 0 ] [ _ ] [ _ ] [ _ ] \|<br>\|                                    \|<br>\|  ⏳ Token Expires In: 04:52        \|<br>\|                                    \|<br>\|       ======================       \|<br>\|       \|\|  VERIFY & ACCOUNT   \|\|       \|<br>\|       ======================       \|<br>\|                                    \|<br>\|  Didn't receive code? [Resend SMS] \|<br>📱 ---------------------------------- 📱</pre> | **1. Token Input Fields:**<br>• Component: 6 individual split text-boxes.<br><br>**2. Countdown Timer Block:**<br>• Logic: Automatically counts down from 05:00 minutes. If reaching 00:00, triggers `NFR-SEC-03` to wipe tokens.<br><br>**3. Resend Hyperlink:**<br>• Action: Re-invokes `FR-01` and resets countdown clock parameters. Disabled for 60 seconds post-click. |

---

### Screen C: Profile Ingestion & IDV Upload UI (US-02 / US-03)
*Purpose: Data collection layout and asynchronous verification injection point.*

| User Interface Component Layout | Component Metadata & Actions |
| :--- | :--- |
| <pre>📱 ---------------------------------- 📱<br>\| < Back            Profile Setup    \|<br>+------------------------------------+<br>\|                                    \|<br>\|       [ 📷 Upload Profile Image ]  \|<br>\|                                    \|<br>\|  First Name:        Last Name:     \|<br>\|  [ Naveen     ]     [ Shanmugam  ] \|<br>\|                                    \|<br>\|  About Me / Short Bio (Optional):  \|<br>\|  [ I want to support seniors with ]\|<br>\|  [ grocery pick-ups and pharmacy  ]\|<br>\|                                    \|<br>\|  Select Support Capabilities:       \|<br>\|  [X] Grocery Run     [X] Rx Delivery\|<br>\|  [ ] Dog Walking     [ ] Home Chores \|<br>\|                                    \|<br>\|  Identity Verification (Required): \|<br>\|  +------------------------------+  \|<br>\|  \| [🖼️] DRIVER LICENSE / PASSPORT  \|  \|<br>\|  \| File Size Restriction: Max 5MB \|  \|<br>\|  +------------------------------+  \|<br>\|                                    \|<br>\|       ======================       \|<br>\|       \|\| INITIALIZE ACCOUNT  \|\|       \|<br>\|       ======================       \|<br>📱 ---------------------------------- 📱</pre> | **1. Core Profile Text Inputs:**<br>• Maximum character validation limits: 50 characters for name inputs, 300 characters for bio inputs.<br><br>**2. Capability Identifiers:**<br>• Component: Custom layout Checkbox tags allowing multi-selection configurations.<br><br>**3. Document Upload Target Area:**<br>• Event: Restricts ingestion formats to `.jpg`, `.jpeg`, `.png`. Pushes directly to the `id_image_binary` system field.<br><br>**4. Submission Framework:**<br>• Event: Updates internal system user state variables cleanly to `status=verification_pending`. |
