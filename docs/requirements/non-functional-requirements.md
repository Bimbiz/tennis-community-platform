# Non-Functional Requirements

**Project:** Amateur Tennis Community Platform  
**Document status:** Draft v0.2 — updated after the minor fixes before supervisor's review of 23 October 2026 (NFR-09 raised to Must; NFR-19–NFR-22 added)  
**Related task:** ATC-11  
**Scope:** Initial mobile application and backend release

## 1. Purpose

This document specifies measurable quality requirements for the amateur tennis mobile application and its supporting backend. The requirements apply to the core workflows defined in the project proposal: account management, player profiles, tournament registration and management, doubles partner formation, match results, and rating updates.

The numeric targets are **proposed acceptance thresholds**, not measured results or confirmed production service-level commitments. They will be checked against a documented test environment and may be revised with team and supervisor approval before final evaluation.

## 2. Performance

| ID | Requirement | Verification / acceptance criterion | Priority |
|---|---|---|---|
| NFR-01 | Under the agreed test workload, the backend shall respond to common read requests (player profile, tournament list and match history) promptly. | At least 95% of successful requests complete within 1.5 seconds, measured at the API boundary with 30 concurrent simulated users over a 10-minute test. | Must |
| NFR-02 | Tournament registration, result confirmation and rating updates shall complete within a reasonable time under the agreed test workload. | At least 95% of these operations complete within 3 seconds for 30 concurrent simulated users over a 10-minute test; unsuccessful operations are reported separately. | Must |
| NFR-03 | Core application screens shall provide prompt feedback when the user starts a network-dependent action. | During usability testing, an in-progress indicator or relevant feedback becomes visible within 1 second of initiating a network request, including when the server is deliberately delayed. | Should |

## 3. Security and Authentication

| ID | Requirement | Verification / acceptance criterion | Priority |
|---|---|---|---|
| NFR-04 | Protected actions and personal account data shall be accessible only to authenticated users with appropriate permissions. | Authorization tests confirm that unauthenticated requests are rejected and that players cannot edit other players' profiles, manage tournaments they do not organize, or confirm results on behalf of unrelated participants. | Must |
| NFR-05 | Authentication credentials and sensitive information shall be protected in transmission and storage. | Tests and configuration review confirm HTTPS for application-to-server communication, no plaintext passwords in persistent storage or logs, and no secrets committed to the repository. | Must |
| NFR-06 | The system shall resist common input and authorization abuses affecting its core operations. | Negative tests confirm validation of malformed inputs, rejection of unauthorized state changes, and prevention of duplicate rating updates from replayed result-confirmation requests. | Must |
| NFR-19 | Signed-in sessions shall expire and shall be revocable, so that signing out or resetting a password ends access immediately. | Access tokens are valid for at most 30 minutes and carry a session ID that the backend checks on every request; refresh tokens are stored server-side. Tests confirm that a token captured before sign-out or a password reset is rejected with 401 afterwards. | Must |
| NFR-20 | Credentials shall be stored on the device only in the platform's secure storage. | Inspection of a test device confirms that access and refresh tokens are kept only in iOS Keychain / Android Keystore (e.g. through `flutter_secure_storage`), and that no token or password appears in the Drift cache, plain key-value preferences or logs. | Must |
| NFR-21 | Sign-in and account creation shall resist password guessing and weak passwords. | After 5 failed sign-in attempts for one account within 15 minutes, further attempts are blocked for 15 minutes (tested); passwords shorter than 8 characters are rejected; error messages do not reveal whether an email is registered. | Must |

## 4. Privacy and Personal Data

| ID | Requirement | Verification / acceptance criterion | Priority |
|---|---|---|---|
| NFR-07 | The application shall collect only personal information necessary for account, profile and tournament functionality, and clearly distinguish required from optional fields. | Form inspection confirms that optional fields can be left blank and that each required field has a documented purpose. | Must |
| NFR-08 | Personal contact details and precise location, if collected, shall not be exposed to other players by default. | Access-control and interface tests confirm that ordinary users cannot retrieve another user's private contact details or precise location without an explicitly enabled sharing rule. | Must |
| NFR-09 | The application shall provide users with clear information about the handling of their personal data and obtain their consent before collecting it. | A privacy notice is accessible during registration and from account settings, and explains collected data, intended uses, storage location and a contact or process for privacy requests, including account deletion (FR-37). Registration cannot be completed without accepting it. | Must |
| NFR-22 | Distance-based search shall not reveal another player's exact location. | Search results show distance only in coarse bands (for example under 2 km, 2–5 km, 5–10 km, over 10 km) and never coordinates; a test that queries from several positions cannot narrow a player's location below the band size. | Should |

## 5. Usability and Accessibility

| ID | Requirement | Verification / acceptance criterion | Priority |
|---|---|---|---|
| NFR-10 | New users shall be able to complete the basic account and player-profile setup without specialist tennis or technical knowledge. | In a moderated test with at least five participants, at least four complete registration and initial skill self-assessment without assistance; problems are recorded. | Must |
| NFR-11 | Players shall be able to find an appropriate tournament and identify their next scheduled match using understandable navigation and labels. | In a moderated test with at least five participants, at least four complete each assigned task unaided; task completion time and mistakes are recorded. | Must |
| NFR-12 | Important controls and status messages shall remain understandable and usable on supported mobile devices. | Manual tests on at least one Android and one iOS device or simulator confirm readable content, non-overlapping controls, visible errors, and that text scaling to 200% does not block completion of the core tasks. | Should |

## 6. Reliability and Data Integrity

| ID | Requirement | Verification / acceptance criterion | Priority |
|---|---|---|---|
| NFR-13 | Confirmed match results and their associated rating changes shall remain consistent when requests fail or are repeated. | Automated integration tests show that a failed operation does not leave a partially applied rating update, and repeated confirmation requests do not cause additional rating changes. | Must |
| NFR-14 | Temporary network or server failures shall not silently lose user input or present an unsuccessful operation as successful. | With network failure simulated during registration and result submission, the app displays an error or retry option; the backend state is verified before any success message is shown. | Must |
| NFR-15 | The backend shall be recoverable from a stored database backup in the test environment. | A documented restore rehearsal recreates users, tournaments, matches and confirmed ratings from a test backup, with key records checked for consistency. | Should |

## 7. Maintainability and Capacity

| ID | Requirement | Verification / acceptance criterion | Priority |
|---|---|---|---|
| NFR-16 | The mobile and backend components shall be maintainable by the two-person project team without relying on undocumented manual setup. | Repository documentation provides repeatable setup, configuration and test instructions; both developers independently follow the applicable instructions on a clean development environment. | Must |
| NFR-17 | Changes to rating calculations, tournament rules and authorization shall be covered by repeatable automated tests. | The repository contains automated tests for each of these areas, and the tests are executed and recorded before a release candidate is submitted. | Must |
| NFR-18 | The initial system shall support the target evaluation workload without critical errors or data corruption. | A 10-minute test with 30 concurrently active simulated users exercising browsing, registration and result workflows completes with at least 99% successful requests, excluding intentionally invalid requests. | Should |

## 8. Verification Notes

- **Priority:** Must = required for the agreed first release; Should = targeted if time and resources permit. Priorities may be updated during scope review.
- **Performance environment:** Record the mobile device or simulator, server CPU/RAM, database setup, dataset size, network conditions, and load-test tool before reporting results. The proposed workload is an evaluation baseline, not a prediction of real-world demand.
- **Security and privacy:** Verify relevant rules through tests and inspection rather than claiming formal security certification or legal compliance that has not been assessed.
- **Traceability:** Functional requirements describe the operations under test; these NFRs define the quality criteria to apply when verifying them.
- **Open decisions:** Final deployment environment (hosting in Kazakhstan before real users join, see Risk 8), data-retention policy and service-availability target require separate team decisions before production deployment. Account deletion is now specified as FR-37. This draft does not claim any of these have been implemented.
- **Priority change:** NFR-09 was raised from Should to Must in the minor fixes before supervisor's review, because the personal-data mitigation in Risk 8 depends on users accepting the privacy notice at sign-up.

## 9. Relationship to Core Functionality

| Functional area | Relevant NFR IDs |
|---|---|
| Accounts and profiles | NFR-01, NFR-04, NFR-05, NFR-07, NFR-08, NFR-09, NFR-10, NFR-19, NFR-20, NFR-21 |
| Tournament browsing and registration | NFR-01, NFR-02, NFR-03, NFR-11, NFR-12, NFR-14, NFR-18 |
| Matching and doubles team formation | NFR-02, NFR-06, NFR-17, NFR-18, NFR-22 |
| Match results and rating updates | NFR-02, NFR-06, NFR-13, NFR-14, NFR-17 |
| Development and operation | NFR-05, NFR-15, NFR-16, NFR-17, NFR-18 |
